* `NodeNetworkReceiveDrops` - Inbound network packets dropped at node
* `NodeNetworkTransmitDrops` - Outbound network packets dropped at node
* `NodeConntrackTableFull` - The nf_conntrack table is full


## View Cgroups consuming the most resources
```
$ systemd-cgtop
Control Group                                                                                      Tasks   %CPU   Memory  Input/s Output/s
/                                                                                                      -  212.1    50.8G        -        -
/kubepods                                                                                           7193  145.1    24.4G        -        -
/kubepods/burstable                                                                                 4906  142.0    23.5G        -        -
/kubepods/burstable/podbba9e252-d037-11e8-bdf6-5254007264d4                                         1479   99.3    12.0G        -        -
/system.slice                                                                                       2710   61.0    30.0G        -        -
/system.slice/containerd.service                                                                    2040   29.3   796.5M        -        -
/system.slice/kubelet.service                                                                        152   21.9   564.0M        -        -
/kubepods/burstable/podc12c1f65-d038-11e8-bdf6-5254007264d4                                          176   10.6   336.0M        -        -
/system.slice/docker.service                                                                         497   10.1    28.1G        -        -
/kubepods/burstable/podd828d5a6-ad66-11e8-95eb-5254007164d2                                           88    7.1   865.3M        -        -
/user.slice                                                                                            6    6.5    99.2M        -        -
/kubepods/burstable/podc3abd1bc-d038-11e8-bdf6-5254007264d4                                           73    3.7     1.9G        -        -
/kubepods/burstable/pod9d2bb1ab-d038-11e8-bdf6-5254007264d4                                          248    3.5   195.4M        -        -
/kubepods/burstable/podc0d5ff10-d038-11e8-bdf6-5254007264d4                                          112    2.5     1.8G        -        -
/kubepods/burstable/podd96ac2fc-d093-11e8-bdf6-5254007264d4                                           59    2.0    41.5M        -        -
/kubepods/besteffort                                                                                1988    1.8   842.8M        -        -
/kubepods/burstable/pod9aee731d-d038-11e8-bdf6-5254007264d4                                           73    1.7    62.0M        -        -
/kubepods/burstable/pod0a569d2d-ed12-11e7-9a5d-5254007264d6                                          120    1.6   375.5M        -        -
/kubepods/burstable/podd06d770a-d038-11e8-bdf6-5254007264d4                                           92    1.6     1.2G        -        -
/kubepods/burstable/podd96c0d07-d093-11e8-bdf6-5254007264d4                                           40    1.6    32.7M        -        -
```
