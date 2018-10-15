# Coredump

A snapshot of a processes memory and registers at a certain execution point.

## Verify

Verify your Linux supports core dumps -
```
$ zcat /proc/config.gz | grep CONFIG_COREDUMP
CONFIG_COREDUMP=y
```

The kernel can store all of it's [configuration](https://blog.fpmurphy.com/2015/10/what-is-procconfig-gz.html) in a zipped file - `/proc/config.gz`.
