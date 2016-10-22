---
post_title: 'Docker Quick Reference'
layout: post
published: true
---
Docker Quick Reference
======================
[TOC]: #
# Table of Contents
- [Docker Compose Force Rebuild](#docker-compose-force-rebuild)
- [Working With Docker for Mac](#working-with-docker-for-mac)
    - [Aliasing 0.0.0.0 to work around dynamic IPs](#aliasing-0000-to-work-around-dynamic-ips)
    - [Accessing The Xyve Virtual Machine](#accessing-the-xyve-virtual-machine)
    - [Add an Internal Company Registry or Repo](#add-an-internal-company-registry-or-repo)
- [Get Into a Docker Container without docker-enter](#get-into-a-docker-container-without-docker-enter)
- [Get Into a Docker Image which Fails to Start](#get-into-a-docker-image-which-fails-to-start)
- [Free up Disk Space Used by Docker](#free-up-disk-space-used-by-docker)
- [Temporarily Install a Package for Troubleshooting](#temporarily-install-a-package-for-troubleshooting)
- [Run A Container With Env Variables for Testing](#run-a-container-with-env-variables-for-testing)
- [Remove Containers Created and Exited 2 Weeks ago](#remove-containers-created-and-exited-2-weeks-ago)
- [Remove All Exited Containers](#remove-all-exited-containers)
- [Grep Docker stdout and stderr](#grep-docker-stdout-and-stderr)
- [Keep a Container Running](#keep-a-container-running)
- [Run A Container With a Link to Another](#run-a-container-with-a-link-to-another)
- [Logs](#logs)
- [Other References](#other-references)


## Docker Compose Force Rebuild
Also see [here](
http://stackoverflow.com/questions/32612650/how-to-get-docker-compose-to-always-start-fresh-images).

```
docker-compose rm -f
docker-compose pull
docker-compose up --build -d
```

## Working With Docker for Mac

### Aliasing 0.0.0.0 to work around dynamic IPs
To solve this problem: "I want to connect from a container to a service
on the host. The Mac has a changing IP address or no address if you have
no network access". The current recommendation is to attach an unused IP
to the lo0 interface on the Mac eg `sudo ifconfig lo0 alias
10.200.10.1/24`, and make sure your service is listening on this
address or 0.0.0.0 (ie not 127.0.0.1). Then containers can connect to
this address."

So, you need to do this:

```
sudo ifconfig lo0 alias 10.200.10.1/24
```

### Accessing The Xyve Virtual Machine
You might need to do this after restarting/upgrading docker. To get into
the xyve vm use `screen`:
 
```
screen ~/Library/Containers/com.docker.docker/Data/com.docker.driver.amd64-linux/tty
```
The login is 'root', no password.

### Add an Internal Company Registry or Repo

`vi /etc/hosts` and add the address e.g.:

```
10.10.10.100   my-registry.mycompany.com
10.10.10.101   pypi.mycompany.com
```

Exit screen with `Ctrl-a` then `k`.

Here is a `screen` reference: http://ss64.com/osx/screen.html.


## Get Into a Docker Container without docker-enter

```
docker exec -it 963ffd75c1b5 /bin/bash
```

## Get Into a Docker Image which Fails to Start
docker run -it applications_mycontainer /bin/bash
Use `docker images` to find the correct image name 

## Free up Disk Space Used by Docker
See 
http://blog.yohanliyanage.com/2015/05/docker-clean-up-after-yourself/

## Temporarily Install a Package for Troubleshooting
If you need to, you can probably simply install packages in any transient
container, e.g.:

```
apt-get update
apt-get install netcat
nc -v -w3 10.10.10.100 5432
```


## Run A Container With Env Variables for Testing
```
docker run -it -e  MY_ENV_VAR=somevalue myrepo/myapp:latest /bin/bash
```


## Remove Containers Created and Exited 2 Weeks ago

```
docker ps -a | grep "2 weeks" | grep "Exited" | awk '{print $1}' | sudo xargs docker rm
```

## Remove All Exited Containers

```
docker ps -a | grep Exit | awk '{print $1}' |  xargs docker rm
```

## Grep Docker stdout and stderr 
E.g. if you have an application that's writing to both streams and
you're not sure where logs are going: 

```
docker logs 4017b8a68f98 2>&1 | grep
```

## Keep a Container Running 
E.g. if it starts and immediately exits:

```
sudo docker run -t -i my-registry/mycontainer /bin/bash
```

This will attach you directly to the container so you can check the
logs.

```
sudo docker run -d my-registry/my-container /bin/bash
```

This will start it detached.

## Run A Container With a Link to Another

```
docker run --rm -t -i --name mycontainer --link docker_consul_1 my-registry/mycontainer 
```


## Logs
Get the last 20 lines of logs: 

```
docker logs --tail 20 fc805ce579d3
```

## Other References
Cheat sheet: https://github.com/wsargent/docker-cheat-sheet

[wpghs target='view' type='link' text='View and edit this post on GitHub']

