#based on https://gist.github.com/dwilkie/f8d6526edc5f1a8aca385df5113567e4 

## Build docker image

```
$ cd /path/to/Dockerfile
$ sudo docker build .
```

View running processes

```
$ sudo docker ps
```

View all processes

```
$ sudo docker ps -a
```

Run an image in a new container daemonized

```
$ sudo docker run -d <image_name>https://gist.github.com/dwilkie/f8d6526edc5f1a8aca385df5113567e4
```

Run an image in interactive mode with the command `/bin/bash`

```
$ sudo docker run -i -t <image_name> /bin/bash
```

Run an image in interactive mode with the command `/bin/bash` and link the ports.

```
$ sudo docker run -i -t --link <docker_container_name>:<docker_container_alias> <image_name> /bin/bash
```

Run an image with an ENTRYPOINT command in interactive mode with the command `/bin/bash`

```
$ sudo docker run --entrypoint /bin/bash -i -t <image_name>
```

Run an image in interactive mode with the command `/bin/bash` mounting the host director `/var/app/current` to the container directory `/usr/src/app`

```
$ sudo docker run -i -t -v /var/app/current:/usr/src/app/ <image_name> /bin/bash
```

Run an image in interactive mode with the command `/bin/bash` setting the environments variables `FOO` and `BAR`

```
$ sudo docker run -i -t -e FOO=foo -e BAR=bar <image_name> /bin/bash
```

## Getting started with nvidia-docker 

# If you have nvidia-docker 1.0 installed: we need to remove it and all existing GPU containers
```
docker volume ls -q -f driver=nvidia-docker | xargs -r -I{} -n1 docker ps -q -a -f volume={} | xargs -r docker rm -f
sudo apt-get purge -y nvidia-docker
```
# Add the package repositories
```
curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey | \
  sudo apt-key add -
distribution=$(. /etc/os-release;echo $ID$VERSION_ID)
```
```
curl -s -L https://nvidia.github.io/nvidia-docker/$distribution/nvidia-docker.list | \
  sudo tee /etc/apt/sources.list.d/nvidia-docker.list
```
```
sudo apt-get update
```

# Install nvidia-docker2 and reload the Docker daemon configuration
```
sudo apt-get install -y nvidia-docker2
```
```
sudo pkill -SIGHUP dockerd
```

# Test nvidia-smi with the latest official CUDA image
```
docker run --runtime=nvidia --rm nvidia/cuda:9.0-base nvidia-smi
```


## Change image storage directory 

#base on https://forums.docker.com/t/how-do-i-change-the-docker-image-installation-directory/1169

Using a symlink is a method to change image storage.

Caution - These steps depend on your current /var/lib/docker being an actual directory (not a symlink to another location).

Stop docker: 
```
service docker stop
```
Verify no docker process is running ```ps faux```
Double check docker really isn’t running. 

Take a look at the current docker directory: 
```
ls /var/lib/docker/
```
2b) Make a backup - 
```
tar -zcC /var/lib docker > /mnt/pd0/var_lib_docker-backup-$(date +%s).tar.gz
```

Move the /var/lib/docker directory to your new partition: 
```
mv /var/lib/docker /mnt/pd0/docker

```
Make a symlink: 
```
ln -s /mnt/pd0/docker /var/lib/docker
```

Take a peek at the directory structure to make sure it looks like it did before the mv: ```ls /var/lib/docker/``` (note the trailing slash to resolve the symlink)
Start docker back up 
```
service docker start
```
restart your containers
