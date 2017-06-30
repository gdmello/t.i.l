# AutoUpdates
CoreOS Container Linux philisophy includes auto-updates. These are handles via the `locksmith` daemon. This daemon is accessible via a commandline utility, `locksmitctl`.
Docs are [here](https://github.com/coreos/locksmith).
`locksmith` supports 3 update strategies-
* `etcd-lock` (default) - acquire a lock, before rebooting the machine for an update. The lock is obtained from an ectd cluster (key `coreos.com/updateengine/rebootlock/semaphore`). The default number of machines which can be concurrently booted is [1](https://github.com/coreos/locksmith#maximum-semaphore)
* `reboot` - machine reboots immediately once an update has been downloaded.
* `off` - machine never reboots, reboot has to be manually triggered.

The chosen reboot strategy can be configured [here](https://github.com/coreos/locksmith#configuration).
In `/etc/coreos/update.conf`-
```
REBOOT_STRATEGY=reboot
```

## `etcd-lock` strategy
If using the `etcd-lock` strategy, and if you need to modify the `locksmithd` (locksmith daemon) config after boot, add a systemd drop-in and reload systemd, `systemctl daemon-restart` and finally restart the locksmith daemon, `systemctl restart locksmithd.service`. See full [description](https://coreos.com/os/docs/latest/using-systemd-drop-in-units.html).
