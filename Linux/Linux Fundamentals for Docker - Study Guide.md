

A structured reference covering the Linux internals you need before diving into Docker: processes, signals, permissions, mounts, `/proc`, and namespaces.

---

## 1. Processes, Parent-Child Relationships, and PIDs

### Core concepts

- A **process** is a running instance of a program. Every process has a unique **PID** (Process ID).
- Every process (except PID 1) has a **parent process**, identified by its **PPID** (Parent Process ID).
- The very first process started by the kernel at boot is **PID 1** (historically `init`, on modern systems usually `systemd`). It is the ancestor of every other process.
- When a process starts another process, it does so via `fork()` (creates a copy of itself) followed by `exec()` (replaces that copy's memory with the new program). This is why child processes inherit environment variables, open file descriptors, and permissions from their parent.
- If a parent dies before its child, the child becomes an **orphan** and is "re-parented" to PID 1 (or the nearest subreaper).
- A process that has finished executing but still has an entry in the process table (because its parent hasn't read its exit status) is called a **zombie**.

### Process states

|State|Meaning|
|---|---|
|R|Running or runnable|
|S|Sleeping (waiting for an event)|
|D|Uninterruptible sleep (usually I/O)|
|T|Stopped (e.g. by `SIGSTOP`)|
|Z|Zombie|

### Useful commands

```bash
ps aux              # Snapshot of all processes (BSD style)
ps -ef               # Snapshot of all processes (UNIX style, shows PPID)
ps --forest          # Show process tree using ps
pstree               # Visual tree of parent-child relationships
pstree -p            # Include PIDs in the tree
echo $$              # PID of the current shell
echo $PPID           # PPID of the current shell
```

### Why this matters for Docker

A container is, at its core, just a **process tree** isolated from the host using namespaces. Understanding PID 1 is critical — the process you specify as `ENTRYPOINT`/`CMD` in a Dockerfile becomes **PID 1 inside the container's PID namespace**, which has special responsibilities (like reaping zombies and handling termination signals).

---

## 2. Inspecting and Controlling Processes

### `ps` — snapshot of processes

```bash
ps aux                        # all processes, all users
ps aux --sort=-%cpu           # sorted by CPU usage
ps aux --sort=-%mem           # sorted by memory usage
ps -p <PID> -o pid,ppid,cmd   # custom columns for a specific PID
```

### `top` — live, interactive process viewer

```bash
top
```

Key interactive commands inside `top`:

- `P` — sort by CPU usage
- `M` — sort by memory usage
- `k` — kill a process (prompts for PID and signal)
- `1` — toggle per-core CPU view
- `q` — quit

### `htop` — improved, colorized version of `top`

```bash
sudo apt install htop   # if not installed
htop
```

- Scrollable, mouse-friendly, shows a visual process tree with `F5`.
- `F9` to send a signal to a selected process directly from the UI.

### `kill` — send a signal to a process by PID

```bash
kill <PID>              # sends SIGTERM by default
kill -9 <PID>            # sends SIGKILL (force kill)
kill -SIGHUP <PID>       # sends SIGHUP by name
kill -l                  # list all available signals
```

### `pkill` / `killall` — send a signal by process name

```bash
pkill nginx              # SIGTERM to all processes named "nginx"
pkill -9 -f "python app.py"   # SIGKILL matching full command line
killall node             # SIGTERM to all "node" processes
```

### Other useful inspection tools

```bash
jobs                      # background jobs in current shell
fg / bg                   # bring job to foreground/background
nice -n 10 <command>       # start a process with lower priority
renice -n 5 -p <PID>       # change priority of a running process
lsof -p <PID>              # files opened by a process
```

---

## 3. Linux Signals

Signals are software interrupts sent to a process to notify it of an event. A process can choose to **catch**, **ignore**, or let the **default action** occur (except for a couple of signals that can never be caught).

|Signal|Number|Default Action|Use Case|
|---|---|---|---|
|`SIGTERM`|15|Terminate|Polite request to shut down; process can catch it and clean up (close files, flush buffers, save state) before exiting. This is what `kill` sends by default and what Docker sends first on `docker stop`.|
|`SIGKILL`|9|Terminate|Immediate, forceful termination. **Cannot be caught, blocked, or ignored.** The kernel kills the process outright — no cleanup happens. Use only when a process is unresponsive.|
|`SIGINT`|2|Terminate|Sent when you press `Ctrl+C` in a terminal. Interrupts a foreground process; catchable, so many programs use it to exit gracefully.|
|`SIGHUP`|1|Terminate|Originally sent when a terminal closed ("hang up"). Now commonly repurposed by daemons to mean "reload your configuration file without restarting" (e.g. `nginx`, `sshd`).|
|`SIGSTOP`|19|Stop|Pauses a process. Cannot be caught (like `SIGKILL`).|
|`SIGCONT`|18|Continue|Resumes a stopped process.|

### Practical guidance: when to use which

1. **Always try `SIGTERM` first.** It gives the application a chance to shut down cleanly — close database connections, finish in-flight requests, delete temp files.
2. **Escalate to `SIGKILL` only if the process ignores `SIGTERM`** or is hung. This is a last resort since it skips all cleanup.
3. **Use `SIGHUP`** when you want a long-running daemon to reload config without a full restart (check the tool's docs — not all programs honor this convention).
4. **`SIGINT`** is mostly relevant for interactive/foreground processes you're running yourself in a terminal.

### Sending signals

```bash
kill -SIGTERM <PID>     # or: kill -15 <PID>
kill -SIGKILL <PID>      # or: kill -9 <PID>
kill -SIGHUP <PID>       # or: kill -1 <PID>
```

### Why this matters for Docker

- `docker stop` sends `SIGTERM`, waits a grace period (default 10s), then sends `SIGKILL` if the container hasn't exited.
- `docker kill` sends `SIGKILL` (or a custom signal) immediately.
- If your container's PID 1 doesn't properly handle/forward `SIGTERM` (common with shell-script entrypoints or `sh -c`), `docker stop` can hang for the full timeout and then force-kill, causing unclean shutdowns. This is why tools like `tini` or `dumb-init` are often used as an init process inside containers.

---

## 4. File Permissions, Ownership, and umask

### The permission model

Every file/directory has three permission sets, for three categories of user:

```
-rwxr-xr--  1 alice  devs  4096 Sep 3 10:00 script.sh
 │││ │││ │││
 │││ │││ └── other (world): r--  (read only)
 │││ └────── group: r-x  (read + execute)
 └────────── owner: rwx  (read + write + execute)
```

- `r` = read (4), `w` = write (2), `x` = execute (1)
- First character: `-` file, `d` directory, `l` symlink

### Viewing and changing ownership

```bash
ls -l file.txt              # view permissions and owner:group
chown alice file.txt        # change owner
chown alice:devs file.txt   # change owner and group
chgrp devs file.txt          # change group only
chown -R alice:devs dir/     # recursive
```

### `chmod` — changing permissions

**Symbolic mode:**

```bash
chmod u+x script.sh      # add execute for owner
chmod g-w file.txt       # remove write for group
chmod o=r file.txt       # set "other" to read-only
chmod a+r file.txt       # add read for all (owner, group, other)
```

**Numeric (octal) mode** — sum of r(4)+w(2)+x(1) per category:

```bash
chmod 755 script.sh      # rwxr-xr-x  (owner: rwx, group: r-x, other: r-x)
chmod 644 file.txt       # rw-r--r--  (common for regular files)
chmod 700 private/       # rwx------  (owner-only access)
```

### `umask` — default permission mask

`umask` controls the **default** permissions new files/directories get, by subtracting from the maximum:

- Max for files: `666` (rw-rw-rw-, files don't get execute by default)
- Max for directories: `777` (rwxrwxrwx)

```bash
umask               # view current mask, e.g. 0022
umask 0027           # set a new mask for this shell session
```

With `umask 022`: new files → `666 - 022 = 644`, new directories → `777 - 022 = 755`.

### Special permission bits

```bash
chmod u+s file        # SUID — run as file owner, not the invoking user
chmod g+s dir/         # SGID — new files in dir inherit its group
chmod +t dir/          # Sticky bit — only owner can delete their own files (e.g. /tmp)
```

### Why this matters for Docker

- Files created inside a container are owned by whatever UID the container process runs as — by default often `root (0)`, which is a security concern.
- Bind-mounted host directories keep their host ownership/permissions; UID mismatches between host and container are a very common source of "permission denied" errors.
- Best practice: run containers as a non-root user (`USER` in Dockerfile) and align UIDs between host and container when bind-mounting.

---

## 5. Mount Points, Filesystems, and Bind Mounts

### What is a mount?

Linux presents **all storage as a single unified tree** rooted at `/`. A **mount** attaches a filesystem (a disk partition, a virtual filesystem, or even another directory) onto a directory (the **mount point**) in that tree, making its contents accessible there.

```bash
mount                    # list all current mounts
mount | column -t         # more readable
df -h                     # disk usage per mounted filesystem
lsblk                     # block devices and their mount points
findmnt                   # tree view of mounts
```

### Mounting and unmounting

```bash
sudo mount /dev/sdb1 /mnt/data      # mount a device at a mount point
sudo umount /mnt/data                # unmount
cat /proc/mounts                     # kernel's live view of all mounts
cat /etc/fstab                       # persistent mounts configured at boot
```

### Bind mounts — the key concept for Docker

A normal mount attaches a _device/filesystem_ to a directory. A **bind mount** instead attaches **one directory (or file) on the same filesystem to another location** — it's like a portal: both paths point to the exact same underlying data.

```bash
sudo mount --bind /host/path /target/path
```

- No new filesystem is created — you're just making existing data visible at a second path.
- Changes made through either path are instantly visible through the other, because they reference the same inode.
- Can be made read-only: `mount --bind -o ro /host/path /target/path`

### Why bind mounts are essential for Docker

Docker's `-v` / `--mount type=bind` flag uses exactly this Linux feature:

```bash
docker run -v /host/app:/app my-image
```

This bind-mounts the host's `/host/app` directory into the container's filesystem at `/app`. It's how:

- Source code on your host stays live-editable inside a running container (great for local dev).
- Containers can persist data outside their own writable layer.
- Multiple containers can share the same host directory.

Docker also has **named volumes** (managed by Docker in `/var/lib/docker/volumes/`, better for portability/production) and **tmpfs mounts** (RAM-only, for sensitive/ephemeral data) — but bind mounts are the most direct expression of raw Linux mount mechanics.

### Container root filesystems, conceptually

A container's root filesystem is itself built by **layering filesystems together** (using OverlayFS, a union filesystem) and then presenting the combined result as the container's `/`. This is a more advanced mount concept you'll meet directly when studying Docker's storage drivers.

---

## 6. The `/proc` Virtual Filesystem

`/proc` is not a real filesystem on disk — it's a **virtual filesystem** generated by the kernel in real time, exposing kernel and process information as if it were files. Reading these "files" queries live kernel state; nothing is stored on disk.

### System-wide information

```bash
cat /proc/cpuinfo        # CPU details (model, cores, flags)
cat /proc/meminfo         # memory usage (total, free, cached, etc.)
cat /proc/loadavg         # system load averages
cat /proc/uptime          # system uptime in seconds
cat /proc/version         # kernel version
cat /proc/filesystems     # filesystems supported by the kernel
cat /proc/mounts          # currently mounted filesystems (live)
cat /proc/interrupts      # interrupt counts per CPU
```

### Networking

```bash
cat /proc/net/dev          # network interface statistics
cat /proc/net/tcp          # active TCP connections (raw, numeric)
cat /proc/net/route        # kernel routing table
```

### Per-process information: `/proc/<PID>/`

Every running process gets its own directory, e.g. `/proc/1234/`:

```bash
cat /proc/1234/status      # human-readable status: state, memory, UID/GID, etc.
cat /proc/1234/cmdline      # the exact command line used to start it
ls -l /proc/1234/fd/        # open file descriptors (symlinks to actual files/sockets)
cat /proc/1234/environ      # environment variables (null-separated)
readlink /proc/1234/cwd     # current working directory
readlink /proc/1234/exe     # path to the executable binary
cat /proc/1234/limits       # resource limits (ulimits) in effect
cat /proc/1234/maps         # memory-mapped regions
```

### Handy self-reference

```bash
cat /proc/self/status       # info about whatever process is reading it
```

### Why this matters for Docker

- Tools like `docker stats`, `top`, and `htop` all ultimately read `/proc` under the hood.
- Container resource limits (CPU/memory) set via `docker run --memory` / `--cpus` are enforced using **cgroups**, and you can inspect their effect through `/sys/fs/cgroup/` and cross-reference with `/proc/<PID>/`.
- Containers get their **own isolated view of `/proc`** (e.g. `/proc/1` inside a container is the container's own PID 1, not the host's) — this isolation is provided by the **PID namespace**, which leads directly into the next topic.

---

## 7. Namespaces — the Foundation of Containers

A **namespace** is a Linux kernel feature that wraps a global system resource in an abstraction, making it appear to a process (and its children) as if it has its own **isolated instance** of that resource — while other processes on the same machine see a different instance (or the unrestricted whole).

This is the single most important Linux concept for understanding Docker: **a container is just a regular Linux process with a restricted view of the system, created using namespaces (for isolation) and cgroups (for resource limits).** There is no "container" object in the kernel — it's a userspace concept built entirely on these primitives.

### The main namespace types

|Namespace|Isolates|Effect inside a container|
|---|---|---|
|**PID**|Process IDs|Container sees its own process tree starting at PID 1; can't see host processes.|
|**NET**|Network stack|Container gets its own network interfaces, IP addresses, routing table, ports.|
|**MNT**|Mount points|Container has its own filesystem view/root — separate from the host's mounts.|
|**UTS**|Hostname & domain name|Container can have its own hostname without affecting the host.|
|**IPC**|Inter-process communication (shared memory, semaphores)|Container's IPC objects are invisible to the host and other containers.|
|**USER**|User & group IDs|Container process can be "root" inside the namespace while mapping to an unprivileged user on the host.|
|**CGROUP**|Cgroup root directory view|Container sees its own cgroup hierarchy root.|

### Inspecting namespaces

```bash
ls -l /proc/<PID>/ns/          # list the namespaces a process belongs to
lsns                            # list all namespaces on the system
sudo unshare --pid --net --mount --fork bash   # manually create new namespaces (experiment!)
```

### Namespaces + cgroups = containers

- **Namespaces** answer: _"What can this process see?"_ (isolation)
- **cgroups** (control groups) answer: _"How much can this process use?"_ (CPU, memory, I/O limits)

Docker (via `containerd` and `runc`) combines both when it starts a container:

1. Creates a new set of namespaces for the container process.
2. Sets up cgroup limits according to `docker run` flags.
3. Sets up the container's root filesystem (via mount namespace + OverlayFS layers).
4. Execs your `ENTRYPOINT`/`CMD` as PID 1 inside that isolated environment.

Understanding this makes Docker far less "magic" — it's Linux processes, given a curtain to sit behind.

---

## Suggested Practice Before the Docker Sessions

1. Run a background process, find its PID with `ps`, and practice `kill -SIGTERM` vs `kill -9` on it. Observe the difference in `/proc/<PID>/status` before it dies.
2. Create a file, then experiment with `chmod` (both symbolic and numeric) and `chown`, and check the resulting permission string with `ls -l`.
3. Create two directories, bind-mount one into the other with `mount --bind`, create a file in one, and confirm it appears in both.
4. Explore `/proc/<PID>/ns/` for a couple of different running processes (e.g., your shell vs. a system daemon) and compare namespace IDs.
5. Run `unshare --pid --fork --mount-proc bash` and run `ps aux` inside it — notice you only see a tiny process tree, giving you a hands-on feel for what Docker does under the hood.

---

_This guide is meant as a foundation. The next sessions on Docker internals will build directly on namespaces, cgroups, OverlayFS, and the container runtime (runc/containerd) using these concepts as the base layer._