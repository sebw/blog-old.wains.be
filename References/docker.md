# Docker useful commands

#### Get Docker version

`docker version`

#### Download hello-world image and execute

`docker run hello-world`

#### Image nginx on port 80

-d : detach. Run in background
-p : publish a containers port(s) to the host

`docker run -d -p 80:80 --name webserver nginx`

#### List running containers

`docker ps`

#### List all containers (running or stopped)

`docker ps -a`

#### Get info (like IP address) from container

`docker inspect <container ID>`

#### Stop/start a container

```
docker stop webserver
docker start webserver
```

#### Troubleshoot a container not starting

`docker logs name_of_container`

#### Execute commands in the container

`docker exec -it "name of container" bash`

#### Delete a container

`docker rm -f webserver`

#### List images

`docker images`

#### Delete an image

`docker rmi nginx`

#### List networks

`docker network ls`

#### Assign a static IP to a container

```
docker network create --subnet=172.18.0.0/16 mynet123  
docker run --net mynet123 --ip 172.18.0.22 -it ubuntu bash  
```

#### Start a container with environment variables

`docker run --name ssl_revproxy -e CERTS=hostname.example.org -e EMAIL=john.doe@example.org -v /etc/ssl/dhparam:/etc/ssl/dhparam -v /srv/letencrypt:/etc/letsencrypt -p 8081:80 -p 443:443 bradjonesllc/docker-nginx-letsencrypt`

#### Start an nginx container

`docker run -d -p 80:80 --name webapp01 -v /some/content:/usr/share/nginx/html:ro nginx`

#### Create a custom image based on CentOS

```
docker run -it centos /bin/bash (will download and enter the image immediately)
Make some changes on the image, for example "mkdir /srv/salt"
docker commit $id_du_conteneur sebastienw/centos7-salt
```

#### Start a CentOS image

`docker run --privileged -it --name test centos /bin/bash`