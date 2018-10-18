# Performance System Calls

http://www.brendangregg.com/Perf/linux_perf_tools_full.png

# strace
Debug all the system calls made by a program. Slows down a program, as it pauses the program before and after each system call.
System [calls](http://www.brendangregg.com/blog/2014-05-11/strace-wow-much-syscall.html)

# Coredump

A snapshot of a processes memory and registers at a certain execution point.

## Verify

Verify your Linux supports core dumps -
```
$ zcat /proc/config.gz | grep CONFIG_COREDUMP
CONFIG_COREDUMP=y
```

The kernel can store all of it's [configuration](https://blog.fpmurphy.com/2015/10/what-is-procconfig-gz.html) in a zipped file - `/proc/config.gz`.

The location for this core dump file can be found in -
```
$ cat /proc/sys/kernel/core_pattern
|/usr/lib/systemd/systemd-coredump %P %u %g %s %t %c %e
```
On CoreOS this is set in `/usr/lib/sysctl.d/50-coredump.conf` -
```
$ cat /usr/lib/sysctl.d/50-coredump.conf 
#  This file is part of systemd.
#
#  systemd is free software; you can redistribute it and/or modify it
#  under the terms of the GNU Lesser General Public License as published by
#  the Free Software Foundation; either version 2.1 of the License, or
#  (at your option) any later version.

# See sysctl.d(5) for the description of the files in this directory,
# and systemd-coredump(8) and core(5) for the explanation of the
# setting below.

kernel.core_pattern=|/usr/lib/systemd/systemd-coredump %P %u %g %s %t %c %e
```

## How to core dump
Once core dump is enabled on a system, a core dump can be created by -

### Program Crash
```
$ ./myprogram
Floating point exception (core dumped)
```

### Kill a running process
Kill a process by [sending](https://linux-audit.com/understand-and-configure-core-dumps-work-on-linux/) the <em>segmentation violation</em>, aka <em>segmentation fault</em> (accessing memory which is not availalbe/ restricted)-
```
$ kill -s SIGSEGV PID
```

### Using gdb


## View Core Dumps
```
$ sudo coredumpctl list
```

## Example
Generating a core dump for the kubelet (kyperkube executable) in a CoreOS node (Tectonic spun Kubernetes node)-
```
// Assuming only kubelet process is running as a rkt pod, find and enter the pod
$ rkt enter `rkt list --format=json | jq .[0].name -r`
# apt-get update && apt-get install -y gdb
# gcore -o /var/log/core-hyperkube `pgrep kubelet` 
//inspect the core dump file via gdb
# gdb /hyperkube /var/log/core-hyperkube.<kubelet_PID>
```
## gdb
[What can you do with gdb?](http://www.brendangregg.com/blog/2016-08-09/gdb-example-ncurses.html)
[Debugging with gdb](http://mermaja.act.uji.es/docencia/is37/data/gdb.pdf)

## References
https://jvns.ca/blog/2018/04/28/debugging-a-segfault-on-linux/
http://www.brendangregg.com/blog/2016-08-09/gdb-example-ncurses.html

# Debugging Docker Containers
Two approaches described [here](https://blog.wnohang.net/index.php/2015/05/05/debugging-docker-containers-with-gdb-and-nsenter/).

## Force a stack trace to be logged
[Force stack trace](https://docs.docker.com/config/daemon/#force-a-stack-trace-to-be-logged)
From @raj.perera-
```
pgrep -f /kubelet | xargs -I{} bash -c 'cat /proc/{}/task/*/stack'
pgrep -f /kubelet | xargs -I{} bash -c 'ls -1 /proc/{}/task/ | xargs -I% bash -c "echo --- pid {} task % ---; cat
```

# Awesome References

[Linux debugging tools I love - Julia Evans](https://jvns.ca/blog/2016/07/03/debugging-tools-i-love/)
