Proxy
-----
`http_proxy` environment variable can be used to proxy http requests

Search for a process by name
------------------------------
`pgrep -n 1 etcd`

Send SIGHUP signal to a process
-------------------------------
```kill SIGHUP `pgrep etcd` ```

Default file permissions for new files
--------------------------------------
`umask` - The user file-creation mode mask (umask) is use to determine the file permission for newly created files.
In the Octal format it is `022`-
Octal value : Permission
* 0 : read, write and execute
* 1 : read and write
* 2 : read and execute
* 3 : read only
* 4 : write and execute
* 5 : write only
* 6 : execute only
* 7 : no permissions

In symbolic format it is -
`umask u=rwx,g=,o=`
https://www.cyberciti.biz/tips/understanding-linux-unix-umask-value-usage.html

Remote Characters
-----------------
`kubectl get cm my-config-map | jq '.data.release' | tr -d '"'`
returns the JSON string without quotes.
single quotes are not base64 ecoded.
