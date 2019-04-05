Systemd
=======
An init-system which manages resources as units. Units can be activated via different means-
* socket-based activation - can be used to start services only when the socket (IP address etc) they are attached to receives a request, saving on resources. e.g. - SSHd via socket activation.
* bus-based activation
* path-based activation
* device-based activation
* implicit dependency mapping
* instances and templates
* easy security hardening
* drop-ins and snippets

Descriptions [here](https://www.digitalocean.com/community/tutorials/understanding-systemd-units-and-unit-files).


Useful Commands
===============

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
