# Display File Information
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

# Default file permissions for new files
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

# Create A File Without Vi/Vim
```
$ cat > deployment.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
$ ls 
-rw-rw-r-- 1 gavin.dmello gavin.dmello 98 Feb 28 11:29 deployment.yaml
```
[Source](https://www.howtogeek.com/199687/how-to-quickly-create-a-text-file-using-the-command-line-in-linux/)

# View All Files Still In Use
```
lsof .
COMMAND   PID         USER   FD   TYPE DEVICE SIZE/OFF     NODE NAME
lsof     2611 firstname.lastname  cwd    DIR  259,1     4096 22946902 .
lsof     2612 firstname.lastname  cwd    DIR  259,1     4096 22946902 .
bash    18065 firstname.lastname  cwd    DIR  259,1     4096 22946902 .
code    24216 firstname.lastname  cwd    DIR  259,1     4096 22946902 .
code    24244 firstname.lastname  cwd    DIR  259,1     4096 22946902 .
docker  27056 firstname.lastname  cwd    DIR  259,1     4096 22946902 .
bash    28274 firstname.lastname  cwd    DIR  259,1     4096 22946902 .
bash    28850 firstname.lastname  cwd    DIR  259,1     4096 22946902 .
```

or via 
```
fuser -v .
                     USER        PID ACCESS COMMAND
/home/firstname.lastname/
                     firstname.lastname  18065 ..c.. bash
                     firstname.lastname  24216 ..c.. code
                     firstname.lastname  24244 ..c.. code
                     firstname.lastname  27056 ..c.. docker
                     firstname.lastname  28274 ..c.. bash
                     firstname.lastname  28850 ..c.. bash

```
[Source](https://linuxjourney.com/lesson/tracking-processes-lsof-fuser)
