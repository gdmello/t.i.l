# Search for Package versions (installed/available):

```
$ yum list --show-duplicates docker-ce --disableplugin=versionlock
Loaded plugins: fastestmirror
Repository 'docker-ce-edge' is missing name in configuration, using id
Loading mirror speeds from cached hostfile
 * base: centos.mirror.rafal.ca
 * epel: mirror.csclub.uwaterloo.ca
 * extras: less.cogeco.net
 * updates: centos.mirror.iweb.ca
Installed Packages
docker-ce.x86_64                      3:19.03.1-3.el7                               @docker-ce-stable
Available Packages
docker-ce.x86_64                      17.03.0.ce-1.el7.centos                       docker-ce-stable 
docker-ce.x86_64                      17.03.1.ce-1.el7.centos                       docker-ce-stable 
docker-ce.x86_64                      17.03.2.ce-1.el7.centos                       docker-ce-stable 
docker-ce.x86_64                      17.03.3.ce-1.el7                              docker-ce-stable 
docker-ce.x86_64                      17.06.0.ce-1.el7.centos                       docker-ce-stable 
docker-ce.x86_64                      17.06.1.ce-1.el7.centos                       docker-ce-stable 
docker-ce.x86_64                      17.06.2.ce-1.el7.centos                       docker-ce-stable 
docker-ce.x86_64                      17.09.0.ce-1.el7.centos                       docker-ce-stable 
docker-ce.x86_64                      17.09.1.ce-1.el7.centos                       docker-ce-stable 
docker-ce.x86_64                      17.12.0.ce-1.el7.centos                       docker-ce-stable 
docker-ce.x86_64                      17.12.1.ce-1.el7.centos                       docker-ce-stable 
docker-ce.x86_64                      18.03.0.ce-1.el7.centos                       docker-ce-stable 
docker-ce.x86_64                      18.03.1.ce-1.el7.centos                       docker-ce-stable 
docker-ce.x86_64                      18.06.0.ce-3.el7                              docker-ce-stable 
docker-ce.x86_64                      18.06.1.ce-3.el7                              docker-ce-stable 
docker-ce.x86_64                      18.06.2.ce-3.el7                              docker-ce-stable 
docker-ce.x86_64                      18.06.3.ce-3.el7                              docker-ce-stable 
docker-ce.x86_64                      3:18.09.0-3.el7                               docker-ce-stable 
docker-ce.x86_64                      3:18.09.1-3.el7                               docker-ce-stable 
docker-ce.x86_64                      3:18.09.2-3.el7                               docker-ce-stable 
docker-ce.x86_64                      3:18.09.3-3.el7                               docker-ce-stable 
docker-ce.x86_64                      3:18.09.4-3.el7                               docker-ce-stable 
docker-ce.x86_64                      3:18.09.5-3.el7                               docker-ce-stable 
docker-ce.x86_64                      3:18.09.6-3.el7                               docker-ce-stable 
docker-ce.x86_64                      3:18.09.7-3.el7                               docker-ce-stable 
docker-ce.x86_64                      3:18.09.8-3.el7                               docker-ce-stable 
docker-ce.x86_64                      3:18.09.9-3.el7                               docker-ce-stable 
docker-ce.x86_64                      3:19.03.0-3.el7                               docker-ce-stable 
docker-ce.x86_64                      3:19.03.1-3.el7                               docker-ce-stable 
docker-ce.x86_64                      3:19.03.2-3.el7                               docker-ce-stable 
docker-ce.x86_64                      3:19.03.3-3.el7                               docker-ce-stable 
docker-ce.x86_64                      3:19.03.4-3.el7                               docker-ce-stable 
docker-ce.x86_64                      3:19.03.5-3.el7                               docker-ce-stable 
docker-ce.x86_64                      3:19.03.6-3.el7                               docker-ce-stable 
docker-ce.x86_64                      3:19.03.7-3.el7                               docker-ce-stable 
docker-ce.x86_64                      3:19.03.8-3.el7                               docker-ce-stable 
docker-ce.x86_64                      3:19.03.9-3.el7                               docker-ce-stable 
docker-ce.x86_64                      3:19.03.10-3.el7                              docker-ce-stable 
docker-ce.x86_64                      3:19.03.11-3.el7                              docker-ce-stable 
docker-ce.x86_64                      3:19.03.12-3.el7                              docker-ce-stable 
docker-ce.x86_64                      3:19.03.13-3.el7                              docker-ce-stable
```

# Remove a Package & its Repository Completely From a System
Remove/Uninstall the package "docker-ce" & "docker-ce-cli":
```
$ yum erase -y docker-ce docker-ce-cli
```
Remove package version specification from version lock, if applicable:
```
$ sudo yum versionlock delete docker-*
Loaded plugins: fastestmirror, versionlock
Repository 'docker-ce-edge' is missing name in configuration, using id
Deleting versionlock for: 3:docker-ce-19.03.1-3.el7.*
Deleting versionlock for: 1:docker-ce-cli-19.03.1-3.el7.*
versionlock deleted: 2
```
Remove the repository:
```
$ yum repolist | grep docker
Repository 'docker-ce-edge' is missing name in configuration, using id
docker-ce-stable/7/x86_64     Docker CE Stable - x86_64                       82
$ ll /etc/yum.repos.d/ | grep -i docker
-rw-r--r--. 1 root root 1950 Oct 22 14:52 docker-ce.repo
$ sudo rm -rf /etc/yum.repos.d/docker-ce.repo
```
Clean cache:
```
$ sudo yum clean cache
```
