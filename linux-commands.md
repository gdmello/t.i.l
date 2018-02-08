Proxy
-----
`http_proxy` environment variable can be used to proxy http requests

Search for a process by name
------------------------------
`pgrep -n 1 etcd`

Send SIGHUP signal to a process
-------------------------------
```kill SIGHUP `pgrep etcd` ```

Remote Characters
-----------------
`kubectl get cm my-config-map | jq '.data.release' | tr -d '"'`
returns the JSON string without quotes.
single quotes are not base64 ecoded.

Show/ Manipulate routing, devices, policy routing and tunnels
-------------------------------------------------------------
ip -addr

Print Logs From Kernel Ring Buffer
----------------------------------

dmesg
