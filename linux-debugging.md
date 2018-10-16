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
