View all entries 
```
$ journalctl -xef
```

View all entries by a unit
```
$ journalctl -u locksmith
```

Show files/ drop-ins of one or more units
```
$ systemctl cat locksmithd
```

See status of a service/daemon
```
$ systemctl status locksmithd
```

View environment variables available when a process was run
```
 sudo cat /proc/$(systemctl show -p MainPID locksmithd | sed s/.*=//)/environ
```
