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
indicating an issue between master nodes and etc servers