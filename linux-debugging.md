# Performance System Calls

http://www.brendangregg.com/Perf/linux_perf_tools_full.png

# Trace (strace)
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

## Debugging Docker Containers
Two approaches described [here](https://blog.wnohang.net/index.php/2015/05/05/debugging-docker-containers-with-gdb-and-nsenter/).

## Force a stack trace to be logged
[Force stack trace](https://docs.docker.com/config/daemon/#force-a-stack-trace-to-be-logged)
From @rajiteh-
```
pgrep -f /kubelet | xargs -I{} bash -c 'cat /proc/{}/task/*/stack'
pgrep -f /kubelet | xargs -I{} bash -c 'ls -1 /proc/{}/task/ | xargs -I% bash -c "echo --- pid {} task % ---; cat
```
# Process (/procs)
View details of a running process-
```
$ pgrep kubelet 
810
$ ls -l /procs/810/fd #view all file descriptors used by the project
$ ls -l /procs/810/exe #view the executable
$ ls -l /procs/810/cmdline #view the command line
```
[Source]($ ls -l /procs/810/exe #view trhe executable)

# TCP Dump (tcpdump)
```
$ tcpdump -i any port 53 <-- listen on any interface at port 53 (TCP port)
$ sudo tcpdump -D
1.lxcbr0
2.docker0
3.bluetooth0 (Bluetooth adapter number 0)
4.nflog (Linux netfilter log (NFLOG) interface)
5.nfqueue (Linux netfilter queue (NFQUEUE) interface)
6.eth3
7.any (Pseudo-device that captures on all interfaces)
8.lo [Loopback]
$ tcpdump -i eth0 port 53 # capture packets on a the eth0 device
```

[Source](https://jvns.ca/blog/2017/06/26/3-screencasts/)

## View Cgroups consuming the most resources
```
$ systemd-cgtop
Control Group                                                                                      Tasks   %CPU   Memory  Input/s Output/s
/                                                                                                      -  212.1    50.8G        -        -
/kubepods                                                                                           7193  145.1    24.4G        -        -
/kubepods/burstable                                                                                 4906  142.0    23.5G        -        -
/kubepods/burstable/podbba9e252-d037-11e8-bdf6-5254007264d4                                         1479   99.3    12.0G        -        -
/system.slice                                                                                       2710   61.0    30.0G        -        -
/system.slice/containerd.service                                                                    2040   29.3   796.5M        -        -
/system.slice/kubelet.service                                                                        152   21.9   564.0M        -        -
/kubepods/burstable/podc12c1f65-d038-11e8-bdf6-5254007264d4                                          176   10.6   336.0M        -        -
/system.slice/docker.service                                                                         497   10.1    28.1G        -        -
/kubepods/burstable/podd828d5a6-ad66-11e8-95eb-5254007164d2                                           88    7.1   865.3M        -        -
/user.slice                                                                                            6    6.5    99.2M        -        -
/kubepods/burstable/podc3abd1bc-d038-11e8-bdf6-5254007264d4                                           73    3.7     1.9G        -        -
/kubepods/burstable/pod9d2bb1ab-d038-11e8-bdf6-5254007264d4                                          248    3.5   195.4M        -        -
/kubepods/burstable/podc0d5ff10-d038-11e8-bdf6-5254007264d4                                          112    2.5     1.8G        -        -
/kubepods/burstable/podd96ac2fc-d093-11e8-bdf6-5254007264d4                                           59    2.0    41.5M        -        -
/kubepods/besteffort                                                                                1988    1.8   842.8M        -        -
/kubepods/burstable/pod9aee731d-d038-11e8-bdf6-5254007264d4                                           73    1.7    62.0M        -        -
/kubepods/burstable/pod0a569d2d-ed12-11e7-9a5d-5254007264d6                                          120    1.6   375.5M        -        -
/kubepods/burstable/podd06d770a-d038-11e8-bdf6-5254007264d4                                           92    1.6     1.2G        -        -
/kubepods/burstable/podd96c0d07-d093-11e8-bdf6-5254007264d4                                           40    1.6    32.7M        -        -
```

# Awesome References

[Linux debugging tools I love - Julia Evans](https://jvns.ca/blog/2016/07/03/debugging-tools-i-love/)
