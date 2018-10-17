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
