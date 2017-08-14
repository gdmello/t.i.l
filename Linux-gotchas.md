# remote_storage_adapter not found
Built executable GO binary via - https://github.com/prometheus/prometheus/tree/master/documentation/examples/remote_storage/remote_storage_adapter on ubuntu 14 machine with glibc.

Tried to run it in an alpine docker image.
```
$ ./remote_storage_adapter
/bin/sh: ./remote_storage_adapter: not found
```
```
$ ls -atl
-rwxr-xr-x    1 root     root      12049930 Aug 14 18:43 remote_storage_adapter
```

Learnt `ldd` via colleague and discovered it was looking for external libraraires which do not exist-
```
$ ldd remote_storage_adapter 
	/lib64/ld-linux-x86-64.so.2 (0x7ff335ac2000)
	libpthread.so.0 => /lib64/ld-linux-x86-64.so.2 (0x7ff335ac2000)
	libc.so.6 => /lib64/ld-linux-x86-64.so.2 (0x7ff335ac2000)
$ ls /lib64
ls: /lib64: No such file or directory
```

Solution - run on busybox built with glibc - `busybox:1.27-1:glibc`
```
$ ./remote_storage_adapter -h
Usage of ./remote_storage_adapter:
  -graphite-address string
    	The host:port of the Graphite server to send samples to. None, if empty.
  -graphite-prefix string
    	The prefix to prepend to all metrics exported to Graphite. None, if empty.
  -graphite-transport string
    	Transport protocol to use to communicate with Graphite. 'tcp', if empty. (default "tcp")
  -influxdb-url string
    	The URL of the remote InfluxDB server to send samples to. None, if empty.
  -influxdb.database string
    	The name of the database to use for storing samples in InfluxDB. (default "prometheus")
  -influxdb.retention-policy string
    	The InfluxDB retention policy to use. (default "autogen")
  -influxdb.username string
    	The username to use when sending samples to InfluxDB. The corresponding password must be provided via the INFLUXDB_PW environment variable.
  -log.format value
    	Set the log target and format. Example: "logger:syslog?appname=bob&local=7" or "logger:stdout?json=true" (default "logger:stderr")
  -log.level value
    	Only log messages with the given severity or above. Valid levels: [debug, info, warn, error, fatal]
  -opentsdb-url string
    	The URL of the remote OpenTSDB server to send samples to. None, if empty.
  -send-timeout duration
    	The timeout to use when sending samples to the remote storage. (default 30s)
  -web.listen-address string
    	Address to listen on for web endpoints. (default ":9201")
  -web.telemetry-path string
    	Address to listen on for web endpoints. (default "/metrics")
$
```

