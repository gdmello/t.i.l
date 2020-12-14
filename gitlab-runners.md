# Test Runner Locally
* The gitlab runner (v13.4.1) requires a valid git repository, with a `.gitlab-ci.yml` file prior to running a job locally
* Sample `.gitlab-ci.yml` file:
```
stages:
  - build

mybuildstage:
stage: build
  image: domain.com/images/docker-compose-runner
  script:
    - env | grep -i docker
    - docker version
    - sudo apt-get -y install jq
    - export TOKEN="$(curl "https://auth.docker.io/token?service=registry.docker.io&scope=repository:ratelimitpreview/test:pull" | jq -r .token)"
    - "curl --head -H \"Authorization: Bearer ${TOKEN}\" https://registry-1.docker.io/v2/ratelimitpreview/test/manifests/latest"
    - docker pull alpine:3.11.6
    - "curl --head -H \"Authorization: Bearer ${TOKEN}\" https://registry-1.docker.io/v2/ratelimitpreview/test/manifests/latest"
```
* [Install](https://docs.gitlab.com/runner/install/linux-repository.html#installing-the-runner) the gitlab-runner locally with: 
```
$ curl -L "https://packages.gitlab.com/install/repositories/runner/gitlab-runner/script.deb.sh" | sudo bash
$ apt-cache madison gitlab-runner
$ export GITLAB_RUNNER_DISABLE_SKEL=true; sudo -E apt-get install gitlab-runner=13.4.1
```
* Run job locally without the need for a Gitlab Server with:
```
$ gitlab-runner exec docker --env "DOCKER_AUTH_CONFIG={\"auths\":{\"https://index.docker.io/v1/\":{\"auth\":\"<BASE64_ENCODED_USERNAME:PASSWORD>\"}}}" --docker-volumes /var/run/docker.sock:/var/run/docker.sock builder
Runtime platform                                    arch=amd64 os=linux pid=28832 revision=e95f89a0 version=13.4.1
WARNING: You most probably have uncommitted changes. 
WARNING: These changes will not be tested.         
Running with gitlab-runner 13.4.1 (e95f89a0)
Preparing the "docker" executor
Using Docker executor with image domain.com/images/docker-compose-runner:master ...
Authenticating with credentials from /home/gavin.dmello/.docker/config.json
Pulling docker image domain.com/images/docker-compose-runner:master ...
Using docker image sha256:e2a11f89d384a1738136d9658b0c9285737a858719 for domain.com/images/docker-compose-runner:master with digest domain.com/images/docker-compose-runner@sha256:164985ef1aabfa2f9d9737a3a4cb05cf6985151 ...
Preparing environment
Running on runner--project-0-concurrent-0 via pts-localmachine...
Getting source from Git repository
Fetching changes...
Initialized empty Git repository in /builds/project-0/.git/
Created fresh repository.
Checking out ede92132 as master...

Skipping Git submodules setup
Executing "step_script" stage of the job script
$ env | grep -i docker
CI_JOB_IMAGE=domain.com/images/docker-compose-runner:master
DOCKER_COMPOSE_VERSION=1.15.0
DOCKER_AUTH_CONFIG={"auths":{"https://index.docker.io/v1/":{"auth":"__REDACTED__"}}}
$ docker version
Client:
 Version:           18.06.3-ce
 API version:       1.38
 Go version:        go1.10.3
 Git commit:        d7080c1
 Built:             Wed Feb 20 02:28:55 2019
 OS/Arch:           linux/amd64
 Experimental:      false

Server: Docker Engine - Community
 Engine:
  Version:          19.03.12
  API version:      1.40 (minimum version 1.12)
  Go version:       go1.13.10
  Git commit:       48a66213fe
  Built:            Mon Jun 22 15:44:07 2020
  OS/Arch:          linux/amd64
  Experimental:     false
 containerd:
  Version:          1.2.13
  GitCommit:        7ad184331fa3e55e52b890ea95e65ba581ae3429
 runc:
  Version:          1.0.0-rc10
  GitCommit:        dc9208a3303feef5b3839f4323d9beb36df0a9dd
 docker-init:
  Version:          0.18.0
  GitCommit:        fec3683
$ sudo apt-get -y install jq
Reading package lists...
Building dependency tree...
Reading state information...
The following NEW packages will be installed:
  jq
0 upgraded, 1 newly installed, 0 to remove and 174 not upgraded.
Need to get 102 kB of archives.
After this operation, 283 kB of additional disk space will be used.
Get:1 http://deb.debian.org/debian/ jessie/main jq amd64 1.4-2.1+deb8u1 [102 kB]
debconf: delaying package configuration, since apt-utils is not installed
Fetched 102 kB in 0s (498 kB/s)
Selecting previously unselected package jq.
(Reading database ... 22806 files and directories currently installed.)
Preparing to unpack .../jq_1.4-2.1+deb8u1_amd64.deb ...
Unpacking jq (1.4-2.1+deb8u1) ...
Setting up jq (1.4-2.1+deb8u1) ...
$ export TOKEN="$(curl "https://auth.docker.io/token?service=registry.docker.io&scope=repository:ratelimitpreview/test:pull" | jq -r .token)"
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100  4379    0  4379    0     0  20531      0 --:--:-- --:--:-- --:--:-- 20462
$ curl --head -H "Authorization: Bearer ${TOKEN}" https://registry-1.docker.io/v2/ratelimitpreview/test/manifests/latest
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
  0  2782    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0
HTTP/1.1 200 OK
Content-Length: 2782
Content-Type: application/vnd.docker.distribution.manifest.v1+prettyjws
Docker-Distribution-Api-Version: registry/2.0
Date: Mon, 14 Dec 2020 19:17:02 GMT
Strict-Transport-Security: max-age=31536000
RateLimit-Limit: 100;w=21600
RateLimit-Remaining: 99;w=21600

$ docker pull alpine:3.11.6
3.11.6: Pulling from library/alpine
Status: Image is up to date for alpine:3.11.6
$ curl --head -H "Authorization: Bearer ${TOKEN}" https://registry-1.docker.io/v2/ratelimitpreview/test/manifests/latest
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
  0  2782    0     0    0     0      0      0 --:--:-- --:HTTP/1.1 200 OK    0
Content-Length: 2782
Content-Type: application/vnd.docker.distribution.manifest.v1+prettyjws
Docker-Distribution-Api-Version: registry/2.0
Date: Mon, 14 Dec 2020 19:17:04 GMT
Strict-Transport-Security: max-age=31536000
RateLimit-Limit: 100;w=21600
RateLimit-Remaining: 98;w=21600

--:-- --:--:--     0
Cleaning up file based variables
Job succeeded

```
