Set up Metasploitable2 with Docker 
(for Ubuntu based systems)[^1]

NOTE: This assumes the following scenario:

* Installing/running docker on a remote host (or in a VM)
* I want to expose all the servies outside the container and outside the host
* These commands are all run on the above host/VM
* By putting my account in the docker group, I will not need sudo 

### Install Docker
```
$ sudo apt install docker.io
```

### Hello World for confirmation
```
$ docker run hello-world
```

### Pull the docker image
```
$ docker pull tleemcjr/metasploitable2
```

### See images
```
$ docker images
REPOSITORY                 TAG       IMAGE ID       CREATED       SIZE
tleemcjr/metasploitable2   latest    db90cb788ea1   4 years ago   1.51GB
```

### Fire up new container using the image
NOTE: `--network host` <-- This exposes *ALL* ports

`-p 80:80` would do a single port
```
$ docker run -d --network host -it tleemcjr/metasploitable2 sh -c "/bin/services.sh && bash"
```

### Confirm container is up (netstat can confirm listening ports)
```
$ docker ps
CONTAINER ID   IMAGE                      COMMAND                  CREATED         STATUS         PORTS     NAMES
e26d90fcedc8   tleemcjr/metasploitable2   "sh -c '/bin/service…"   7 seconds ago   Up 7 seconds             boring_burnell
```

### Connect from remote host
```
root@kali ~# curl 172.16.0.106
<html><head><title>Metasploitable2 - Linux</title></head><body>
<pre>
...
```

### Enter shell of container
```
$ docker exec -it boring_burnell bash
root@coconuts:/#
```

## Troubleshooting 
### Container logs
```
$ docker logs boring_burnell
 * Starting web server apache2
 ...
```

### Check status
```
$ docker ps -a
CONTAINER ID   IMAGE                      COMMAND                  CREATED          STATUS          PORTS     NAMES
e26d90fcedc8   tleemcjr/metasploitable2   "sh -c '/bin/service…"   33 minutes ago   Up 33 minutes             boring_burnell
```

## Tear down
### Stop Container
```
$ docker stop boring_burnell
```

### Confirm it stopped
```
$ docker ps -a
CONTAINER ID   IMAGE                      COMMAND                  CREATED          STATUS                        PORTS     NAMES
e26d90fcedc8   tleemcjr/metasploitable2   "sh -c '/bin/service…"   38 minutes ago   Exited (137) 57 seconds ago             boring_burnell
```

### Remove container
```
$ docker rm boring_burnell
```

### Confirm removal
```
$ docker ps -a
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```

### Remove image
```
$ docker rmi tleemcjr/metasploitable2
```

### List images
```
$ docker images
REPOSITORY   TAG       IMAGE ID   CREATED   SIZE
```

## References
https://dockerlabs.collabnix.com/docker/cheatsheet/


[^1]: Current test setup: Ubuntu 20.0.4 Server with docker hosting metasploitable2 inside a VMware VM.
    I was able to set this whole thing up in less than an hour.