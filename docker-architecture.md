# Architecture
```
+--------------+      +---------------+       +-------------------------+
|              |      |               |       |                         |
| docker (cli) +------>dockerd        +------->   containerd            |
|              |      |(docker daemon)|       |                         |
+--------------+      +---------------+       +-------------------------+
                                              | containerd-shim|   runC |
                                              |                |        |
                                              +--------+-------+------+-+
                                                       |              |
                                    2) allow daemonless               |1) start container
                                    containers, so runC|        +-----v------+
                                    can exit/keep      |        |            |
                                    STDIO/FDS open if  +-------->container(s)|
                                    docker/containerd           |            |
                                    die.                        +------------+
```
