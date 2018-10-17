## Namespaces
Linux provides the following [namespaces](http://man7.org/linux/man-pages/man7/namespaces.7.html):

     Namespace   Constant          Isolates
     Cgroup      CLONE_NEWCGROUP   Cgroup root directory
     IPC         CLONE_NEWIPC      System V IPC, POSIX message queues
     Network     CLONE_NEWNET      Network devices, stacks, ports, etc.
     Mount       CLONE_NEWNS       Mount points
     PID         CLONE_NEWPID      Process IDs
     User        CLONE_NEWUSER     User and group IDs
     UTS         CLONE_NEWUTS      Hostname and NIS domain name
       
[PID Namespace](http://man7.org/linux/man-pages/man7/pid_namespaces.7.html)

## Enter a Namespace

With [nsenter](http://man7.org/linux/man-pages/man1/nsenter.1.html)!
```
# Find PID of process, in this case the kubelet
$  ps u -U root  | grep -i " /kubelet"
root     14977 12.6  0.4 1598700 139092 ?      Ssl  Oct16 128:16 /kubelet --kubeconfig=/etc/kubernetes/kubeconfig --require-kubeconfig --cni-conf-dir=/etc/kubernetes/cni/net.d --network-plugin=cni --lock-file=/var/run/lock/kubelet.lock --exit-on-lock-contention --pod-manifest-path=/etc/kubernetes/manifests --allow-privileged --node-labels=node-role.kubernetes.io/node --cni-bin-dir=/var/lib/cni/bin --minimum-container-ttl-duration=6m0s --cluster-dns=10.30.10.30 --cluster-domain=cluster.local --client-ca-file=/etc/kubernetes/ca.crt --cloud-provider= --anonymous-auth=false
$ sudo nsenter -a -t 14977 /bin/bash
beta-c3 / # ps
  PID TTY          TIME CMD
27584 pts/0    00:00:00 sudo
27585 pts/0    00:00:00 nsenter
27586 pts/0    00:00:00 bash
29880 pts/0    00:00:00 ps

```
