# Architecture
## docker architecture
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
[Source](http://alexander.holbreich.org/docker-components-explained/)

## runC architecture-
```
                                      +-------------------+              
                                   /--|OCI config (json)  |              
                               /---   +-------------------+              
                           /---       +---------------------------------+
                       /---         /-|root filesystem                  |
                   /---          /--  |(binaries & libs you wnt to run) |
               /---            /-     +---------------------------------+
+------------<---------------<---------------------------+               
|                                                        |               
|                 runC                                   |               
|       +---------------------------+                    |               
|       |    libcontainer (golang)  |                    |               
+-------+---------------------------+--------------------+               
               |       Container CRUD                            +       
               |       with namespaces, cgroups,                         
               |       capabilities, filesystem access controls          
               |                                                         
+--------------v-----------------------------------------+               
|                  OS                                    |               
|                                                        |               
|                                                        |               
+--------------------------------------------------------+               
                                                                         
```

# example
```
$ docker run --name mariadb -e MYSQL_ROOT_PASSWORD=password -v /data/lists:/var/lib/mysql -d mariadbUnable to find image 'mariadb:latest' locally
latest: Pulling from library/mariadb
...
Digest: sha256:9d443337dfbb2a34583ed7c968cde6115ce1b10630530ff1f0f5c7f1e6f0a76b
Status: Downloaded newer image for mariadb:latest
226d96829523d90ae17e811fc859c666c36a7f03d3562ad58e34c084799f43a9

$ ps axjf | grep docker
18602 23049 23049 18602 pts/4    23049 S+       0   0:00          |   |   \_ sudo dockerd
23049 23050 23049 18602 pts/4    23049 Sl+      0   0:19          |   |       \_ dockerd
23050 23060 23060 23060 ?           -1 Ssl      0   0:06          |   |           \_ docker-containerd --config /var/run/docker/containerd/containerd.toml
23060 24611 24611 23060 ?           -1 Sl       0   0:00          |   |               \_ docker-containerd-shim -namespace moby -workdir /var/lib/docker/containerd/daemon/io.containerd.runtime.v1.linux/moby/226d96829523d90ae17e811fc859c666c36a7f03d3562ad58e34c084799f43a9 -address /var/run/docker/containerd/docker-containerd.sock -containerd-binary /usr/bin/docker-containerd -runtime-root /var/run/docker/runtime-runc
23810 26912 26911 23810 pts/2    26911 S+   1124080248   0:00          |       \_ grep --color=auto docker
```

Evident to see `dockerd -> docker-containerd -> docker-containerd-shim`, where `docker-containerd` & `docker-containerd-shim` are docker wrappers around `containerd` & `containerd-shim`.
