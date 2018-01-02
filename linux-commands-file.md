Display File Information
------------------------
View file stats like groupid, owner id-
```
$ stat /var/run/docker
  File: '/var/run/docker.sock'
  Size: 0         	Blocks: 0          IO Block: 4096   socket
Device: 15h/21d	Inode: 2039        Links: 1
Access: (0660/srw-rw----)  Uid: (    0/    root)   Gid: (  999/  docker)
Context: system_u:object_r:var_run_t:s0
Access: 2018-01-02 16:48:26.702670528 +0000
Modify: 2017-12-30 03:30:39.852864693 +0000
Change: 2018-01-02 16:48:16.265308219 +0000
 Birth: -
```

Used to determine if group id changes took hold after changing docker gid from 233 to 999.
