---
layout: post
title: 'Learning Notes #36 - Active Active / Active Passive Patterns | HA Patterns'
date: 2025-01-04 18:04:20+00:00
render_with_liquid: false
category: Technology
tags:
- HighAvailability
- ClusterManagement
- ActiveActivePattern
- ActivePassivePattern
- WebApplications
---



<p class="wp-block-paragraph"></p><p class="wp-block-paragraph">Today, i learnt about High Availability patterns. Basically on how to handle the clusters for high availability. In this blog i jot down notes on Active Active and Active Passive Patterns for better understanding. </p><p class="wp-block-paragraph"></p><h2 class="wp-block-heading">Active-Active Configuration</h2><p class="wp-block-paragraph">In an <strong>Active-Active</strong> setup, all nodes in the cluster are actively processing requests. This configuration maximizes resource utilization and ensures high throughput. If one node fails, the remaining active nodes take over the load.</p><figure class="wp-block-image size-large"><img alt="" class="wp-image-2324" data-recalc-dims="1" decoding="async" height="737" loading="lazy" src="https://i0.wp.com/parottasalna.com/wp-content/uploads/2025/01/image-40.png?resize=1291%2C737&amp;ssl=1" width="1291"/></figure><h3 class="wp-block-heading"><span style="text-decoration: underline">Example Scenario</span></h3><p class="wp-block-paragraph">Consider a web application with two servers:</p><ol class="wp-block-list" start="1"><li>Server 1: IP 192.168.1.10</li><li>Server 2: IP 192.168.1.11</li><li>Server 3: IP 192.168.1.12</li><li>Server 4: IP 192.168.1.13</li></ol><p class="wp-block-paragraph">Both servers handle incoming requests simultaneously. A load balancer distributes traffic between these servers to balance the load.</p><h3 class="wp-block-heading"><span style="text-decoration: underline">Pros and Cons</span></h3><p class="wp-block-paragraph">Pros:</p><ul class="wp-block-list"><li>Higher resource utilization.</li><li>Better scalability and performance.</li></ul><p class="wp-block-paragraph">Cons:</p><ul class="wp-block-list"><li>Increased complexity in handling data consistency and synchronization.</li><li>Potential for split-brain issues in certain setups.</li></ul><p class="wp-block-paragraph"></p><h3 class="wp-block-heading"><span style="text-decoration: underline">Sample HAProxy config</span></h3><pre class="wp-block-syntaxhighlighter-code">frontend http_front    bind *:80    default_backend http_backdefaults    mode http    timeout connect 5000ms    timeout client 50000ms    timeout server 50000msbackend http_back    balance roundrobin    server server_a 192.168.1.10:80 check    server server_b 192.168.1.11:80 check</pre><p class="wp-block-paragraph"></p><h2 class="wp-block-heading">Active-Passive Configuration</h2><p class="wp-block-paragraph">In an Active-Passive setup, one node (Active) handles all the requests, while the other node (Passive) acts as a standby. If the active node fails, the passive node takes over.</p><figure class="wp-block-image size-large"><img alt="" class="wp-image-2327" data-recalc-dims="1" decoding="async" height="737" loading="lazy" src="https://i0.wp.com/parottasalna.com/wp-content/uploads/2025/01/image-41.png?resize=1291%2C737&amp;ssl=1" width="1291"/></figure><h3 class="wp-block-heading"><span style="text-decoration: underline">Example Scenario</span></h3><p class="wp-block-paragraph">Using the same servers:</p><ol class="wp-block-list" start="1"><li>Server 1: IP 192.168.1.10 (Active)</li><li>Server 2: IP 192.168.1.11 (Active)</li><li>Server 3: IP 192.168.1.12 (Passive)</li><li>Server 4: IP 192.168.1.13 (Passive)</li></ol><p class="wp-block-paragraph">Server B remains idle until Server A becomes unavailable, at which point Server B assumes the active role.</p><h3 class="wp-block-heading"><span style="text-decoration: underline">Pros and Cons</span></h3><p class="wp-block-paragraph">Pros:</p><ul class="wp-block-list"><li>Simplified consistency management.</li><li>Reliable failover mechanism.</li></ul><p class="wp-block-paragraph">Cons:</p><ul class="wp-block-list"><li>Underutilized resources (passive node is idle most of the time).</li><li>Slight delay during failover.</li></ul><p class="wp-block-paragraph"></p><h3 class="wp-block-heading"><span style="text-decoration: underline">Sample HA Proxy Config</span></h3><pre class="wp-block-syntaxhighlighter-code">frontend http_front    bind *:80    default_backend http_backdefaults    mode http    timeout connect 5000ms    timeout client 50000ms    timeout server 50000msbackend http_back    server server_a 192.168.1.10:80 check    server server_b 192.168.1.11:80 check backup</pre>


## Related Posts
- [[Learning Notes #30 - Queue Based Loading | Cloud Patterns]]
- [[Learning Notes #40 - SAGA Pattern | Cloud Patterns]]
- [[Learning Notes #50 - Fixed Partition Pattern | Distributed Pattern]]
- [[Consistent Hashing in Load Balancer]]
- [[Learning Notes #9 - Quorum Queues | RabbitMQ]]

