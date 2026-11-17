---
layout: post
title: Squid Forward Proxy Explained With a Working Setup
date: 2026-11-17 06:30:00+00:00
render_with_liquid: false
category: Networking
tags:
- Squid
- Proxy
- Forward Proxy
- Caching
- Access Control
- Networking
---

## Introduction

Every request your laptop makes to the internet goes straight from your laptop to the website. A forward proxy changes that. The request goes to the proxy first, and the proxy makes the trip on your behalf. Squid is the most widely used open source forward proxy, and it has been around for decades.

In this post we will set up Squid, send real requests through it, block a domain, cache a page, and add a username and password. Every output below came from a real run of Squid 5.7 in a Debian container.

## Forward proxy and reverse proxy in one minute

People often mix up the two, so here is the difference.

| | Forward proxy | Reverse proxy |
|---|---|---|
| Sits in front of | The clients | The servers |
| Who knows about it | The client is configured to use it | The client never knows |
| Typical job | Filter, log and cache outgoing traffic | Load balance and protect incoming traffic |
| Example tools | Squid | Nginx, HAProxy |

If you have followed our HAProxy series, that was the reverse side. Squid is the forward side. It protects the people inside a network from the wider internet, instead of protecting servers from the wider internet.

## Why use a forward proxy

- **Control.** A college or office can decide which sites are reachable and which are not.
- **Logging.** One place records who asked for what and when.
- **Saving bandwidth.** If fifty people open the same page, the proxy fetches it once and serves the other forty nine from memory.
- **One exit address.** All outgoing traffic leaves from the proxy's address, so a firewall only has to trust one machine.

## The configuration

Squid reads one file, `squid.conf`. Here is a small one that does something useful.

```
http_port 3129

acl localnet src 10.0.0.0/8 172.16.0.0/12 192.168.0.0/16 127.0.0.1/32
acl SSL_ports port 443
acl Safe_ports port 80 443
acl CONNECT method CONNECT
acl blocked dstdomain .example.org

http_access deny !Safe_ports
http_access deny CONNECT !SSL_ports
http_access deny blocked
http_access allow localnet
http_access deny all

access_log stdio:/var/log/squid/access.log squid
```

Read it in two halves.

The `acl` lines only give names to things. `localnet` is a list of client addresses. `Safe_ports` is the set of destination ports we allow. `blocked` is every domain ending in `example.org`.

The `http_access` lines are the rules. Squid reads them from top to bottom and the first one that matches wins. That is why the order matters. `deny blocked` must come before `allow localnet`, otherwise a client on the local network would be allowed before the block rule is ever looked at. The final `deny all` makes everything not mentioned a refusal.

## Run it

Install and start Squid in a throwaway container, so nothing on your machine is touched.

```bash
docker run -d --name sqdemo --network host \
  -v $PWD/squid.conf:/etc/squid/squid.conf:ro \
  debian:bookworm-slim sh -c "apt-get update -qq && apt-get install -y squid && \
  mkdir -p /var/log/squid /var/spool/squid && chown -R proxy:proxy /var/log/squid /var/spool/squid && \
  squid -z -N -f /etc/squid/squid.conf; exec squid -N -f /etc/squid/squid.conf"
```

Once it listens on port 3129, point curl at it with the `-x` flag.

```bash
curl -s -o /dev/null -w "%{http_code}\n" -x http://127.0.0.1:3129 http://example.com/
curl -s -o /dev/null -w "%{http_code}\n" -x http://127.0.0.1:3129 http://example.com/
curl -s -o /dev/null -w "%{http_code}\n" -x http://127.0.0.1:3129 http://www.example.org/
curl -s -o /dev/null -w "%{http_code}\n" -x http://127.0.0.1:3129 https://example.com/
curl -s -o /dev/null -w "%{http_code}\n" -x http://127.0.0.1:3129 http://example.com:8080/
```

The five status codes were 200, 200, 403, 200 and 403. The two 403 responses are our own rules. One is the blocked domain and the other is port 8080, which is not in `Safe_ports`.

## Read the access log

The log is where Squid explains itself. This is what those five requests wrote.

```
TCP_MISS/200    GET http://example.com/       HIER_DIRECT/172.66.147.243
TCP_MEM_HIT/200 GET http://example.com/       HIER_NONE/-
TCP_DENIED/403  GET http://www.example.org/   HIER_NONE/-
TCP_TUNNEL/200  CONNECT example.com:443       HIER_DIRECT/172.66.147.243
TCP_DENIED/403  GET http://example.com:8080/  HIER_NONE/-
```

The timestamps, sizes and client address columns are left out here so the lines fit. Each line has a result code, a slash and the HTTP status.

- `TCP_MISS` means the page was not in the cache, so Squid went to the origin. `HIER_DIRECT` confirms it connected straight to the website.
- `TCP_MEM_HIT` is the same URL a moment later. Squid answered from its memory and never contacted the website, which is why the hierarchy column says `HIER_NONE`. In our run the first request took 55 ms and the cached one took 3 ms.
- `TCP_DENIED` is a request our rules refused.
- `TCP_TUNNEL` is the HTTPS request. Squid cannot read encrypted traffic, so it opens a plain tunnel with the `CONNECT` method and passes the bytes through. It can log the host name and size, but never the page content.

That last point trips up many people. A plain Squid can allow or block `example.com:443` as a whole, but it cannot cache or inspect an HTTPS page unless you set up certificate interception, which is a separate and much more sensitive topic.

## Add a username and password

An open proxy on a shared network is an invitation. Squid can ask each client to sign in using a helper program. We use `basic_ncsa_auth` with a password file.

Create a user. Here we use openssl, so no extra package is needed.

```bash
echo "asha:$(openssl passwd -apr1 learn123)" > /etc/squid/passwd
chown proxy /etc/squid/passwd
```

Then add three things to the top of `squid.conf` and swap the allow rule.

```
auth_param basic program /usr/lib/squid/basic_ncsa_auth /etc/squid/passwd
auth_param basic realm Salna proxy
acl authed proxy_auth REQUIRED

http_access allow authed
```

The new `allow authed` line replaces `allow localnet`. Now try three requests.

```bash
curl -s -o /dev/null -w "%{http_code}\n" -x http://127.0.0.1:3130 http://example.com/
curl -s -o /dev/null -w "%{http_code}\n" -x http://127.0.0.1:3130 -U asha:wrong http://example.com/
curl -s -o /dev/null -w "%{http_code}\n" -x http://127.0.0.1:3130 -U asha:learn123 http://example.com/
```

The results were 407, 407 and 200. Status 407 is "proxy authentication required", the proxy version of 401. The log now also records the user name, so the successful line ends with `asha` in the user column.

Basic authentication sends the password in an easily decoded form. Use it only on a network you trust, or put the proxy behind a tunnel.

## Use it from your tools

Most command line tools respect two environment variables.

```bash
export http_proxy=http://asha:learn123@proxy.internal:3129
export https_proxy=http://asha:learn123@proxy.internal:3129
export no_proxy=localhost,127.0.0.1,.internal
```

`no_proxy` lists the destinations that should skip the proxy. Forgetting it is the classic reason a service on the same machine suddenly cannot reach `localhost`.

For Docker, `apt` and `pip` the settings live in their own configuration files, so check each tool when something refuses to connect.

## Mistakes worth avoiding

- **Putting a broad allow rule too early.** Order decides everything. Put denies first, then the narrow allows.
- **Leaving the proxy open to the world.** Always restrict by source network or require a login. Open proxies are found and abused within hours.
- **Allowing every port with CONNECT.** The `deny CONNECT !SSL_ports` rule stops people tunnelling to any port they like through your proxy.
- **Forgetting to reload.** After editing the file run `squid -k parse` to catch typos, then `squid -k reconfigure` to apply it without dropping connections.
- **Expecting to cache HTTPS.** Most of the web is encrypted now, so the cache hit rate is far lower than it was in the early days.

## Summary

A forward proxy is a single door that all outgoing traffic walks through. Squid lets you decide who may use that door, which destinations are allowed, and what gets remembered so it need not be fetched twice. Start with the small configuration above, read the access log until the result codes feel familiar, and add rules one at a time.

## Related Posts

- [[HAProxy EP 4: Understanding ACL - Access Control List]]
