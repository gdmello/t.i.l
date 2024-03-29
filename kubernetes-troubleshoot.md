Issue - debug files on a pod with no terminal access
----------------------------------------------------
Cannot exec into a pod to run a command:
```
$ kcr -n kube-system exec  coredns-bdffbc777-lq9kw cat /etc/resolv.conf
OCI runtime exec failed: exec failed: container_linux.go:345: starting container process caused "exec: \"ls\": executable file not found in $PATH": unknown
command terminated with exit code 126
```
SSH into the host running said pod, and look into the containers layers:
```
$ docker ps | grep -i coredns
f66d796d8273        eb516548c180                             "/coredns -conf /etc…"   4 hours ago         Up 4 hours                              k8s_coredns_coredns-bdffbc777-gc76x_kube-system_91ae6c75-e913-11e9-9a5c-8aa4cb60c64e_0
$ cat /data/docker/containers/f66d796d827329d00e8cb77c7fa1a66b8fdc55f1cf28c748fc3bc219c255c70d/config.v2.json | grep -i resolv.conf
...
"ResolvConfPath":"/data/docker/containers/7f93d7fdb9b7c7db8c46af250ba31cb4358a184c644086b3c0a178534f8a3510/resolv.conf"
...
$ cat /data/docker/containers/7f93d7fdb9b7c7db8c46af250ba31cb4358a184c644086b3c0a178534f8a3510/resolv.conf
nameserver 10.20.321.16
nameserver 10.20.34.99
search domain.com toronto.blah.com
options timeout:1 attempts:5
```

Issue - `kubectl` connectivity issues to apiserver
--------------------------------------------------
This error - 
```
$ kc get nodes
Unable to connect to the server: could not refresh token: invalid character '<' looking for beginning of value
``` 
is caused by the apiserver returning an invalid response.
api-server logs revealed numerous occurrences of this error-
```
W0827 13:26:38.680662       6 controller.go:386] Resetting endpoints for master service "kubernetes" to &{{ } {kubernetes  default /api/v1/namespaces/default/endpoints/kubernetes 79f57e00-ed11-11e7-8861-5254007164d2 69041468 0 2017-12-30 03:28:17 +0000 UTC <nil> <nil> map[] map[] [] nil [] } [{[{10.70.280.41  <nil> <nil>}] [] [{https 443 TCP}]}]}
```
Restarting the kubelet process, kubelet logs revealed this error-
```
user@m7.k8s.domain.com $ sudo journalctl -u kubelet -r
E0827 13:44:42.835893   14041 kubelet_node_status.go:390] Error updating node status, will retry: failed to patch status "{\"status\":{\"$setElementOrder/conditions\":[{\"type\":\"OutOfDisk\"},{\"type\":\"MemoryPressure\
Aug 27 13:44:42 m7.k8s.domain.com kubelet-wrapper[14041]: , diff2={"status":{"$setElementOrder/conditions":[{"type":"OutOfDisk"},{"type":"MemoryPressure"},{"type":"DiskPressure"},{"type":"Ready"}],"conditions":[{"lastHeartbeatTime":"2018-08-27T13:44:42Z","type":"OutOfDisk"},{"l
Aug 27 13:44:42 m7.k8s.domain.com kubelet-wrapper[14041]:  diff1={"metadata":{"annotations":{"container-linux-update.v1.coreos.com/status":"UPDATE_STATUS_CHECKING_FOR_UPDATE"},"resourceVersion":"69045036"},"status":{"$setElementOrder/conditions":[{"type":"OutOfDisk"},{"type":"M
Aug 27 13:44:42 m7.k8s.domain.com kubelet-wrapper[14041]:
```
~indicating an issue between master nodes and etc servers. And sure enough-~
```
$ docker inspect <apiserver container id> | grep -i "etcd-servers"
--etcd-servers=https://etc17.k8s.domain.com:2379,https://etc18.k8s.domain.com:2379,https://etc19.k8s.domain.com:2379,https://etc20.k8s.domain.com:2379,https://etc21.k8s.domain.com:2379",
$ docker inspect <apiserver container id> | grep -i "etcd-cafile"
--etcd-cafile=/etc/kubernetes/secrets/etcd-client-ca.crt
```
The cert file above refers to an in-container path, to determine the host path, run `docker inspect` on the container again and look up the mount-
```
$ docker inspect <apiserver container id> | grep -i ":/etc/kubernetes/secrets"
                "/var/lib/kubelet/pods/82a3f904-ed11-11e7-8861-5254007164d2/volumes/kubernetes.io~secret/secrets:/etc/kubernetes/secrets:ro,Z",
```
Verify connectivity to the etcd node-
```
$ sudo curl https://etc18.k8s.domain.com:2379 --cacert /var/lib/kubelet/pods/82a3f904-ed11-11e7-8861-5254007164d2/volumes/kubernetes.io~secret/secrets/etcd-client-ca.crt
404 page not found
```
~Voila! confirms etcd is not accessible.~
