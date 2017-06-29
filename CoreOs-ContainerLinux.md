# AutoUpdates
CoreOS Container Linux philisophy includes auto-updates. These are handles via the `locksmith` daemon. This daemon is accessible via a commandline utility, `locksmitctl`.
Docs are [here](https://github.com/coreos/locksmith).
`locksmith` supports 3 update strategies-
* `etcd-lock` - acquire a lock, before rebooting the machine for an update. The lock is obtained from an ectd cluster. The default number of machines which can be concurrently booted is [1](https://github.com/coreos/locksmith#maximum-semaphore)
* `reboot` - machine reboots immediately once an update has been downloaded.
* `off` - machine never reboots, reboot has to be manually triggered.
