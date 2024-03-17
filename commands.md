basic commands:

Image
- docker images    OR   docker image list
- docker pull image:tag    OR   docker image pull image:tag
- docker image push username/imagename:tag   (this will push your image to your repo NOTE: need to logged in first)


Container
### NOTE: we can use "docker [option]"   or we can user  "docker container [options]"
- docker create image    OR   docker container create image  (create a container i.e. it'll not start it'll only create a instance of that image)
- docker start cid/cname   OR docker container start cid/cname
- docker run image    OR    docker container run 
- docker run -it image   OR   docker container run -it image  (-i for interactive -t for terminal)
- docker run -d image  (run in background)
- docker run --name [container name] image
- docker run -p [host port]:[container port] -d image
- docker exec -it(for terminal) [container name or id] [command]   (/bin/bash or /bin/sh for terminal)
    example:  docker exec -it 8b134 /bin/bash   (to get ubuntu terminal)
- docker container inspect [container name or id]   (this will show all details about a container)
- docker container stats
- docker container top [conainer name or id]
- docker container logs [options] [conainer name or id]  (-f for live)
- docker run --name [conntainer name] --hostname [host name of container] image
- docker run -d -v [local directory]:[container directory] image  (this will map local directory to container directory to get file sync or to make data persists)
- docker container cp /local/file [container name or id]:/container/location 
- docker run -d -p 172.0.0.1:3000:5000 image  (this will publish the container port 5000 to localhost port 3000, this will not available over local network)
- docker run -d p pcport:contport image    (this will publish container port to all ip associated with network interface in the system this will be available over local network)
- docker run -d -p 192.168.1.36:3000:5000 image  (this will publish container port to the network interface card or local network which is associated to this ip on system)
- docker run -d --expose=8080 -p 80:8080 image  (this will expose the port and publish the port)
- docker run -d --rm image   (auto remove container after task completion)
- 


Troubleshoot
- docker system events --since 60m
- docker container logs [cid/cname]   (it'll show container logs)
- docker container logs -f [cid/cname]   (it'll show container logs and constantly update it)


Images
- docker image history [image name]   (it'll show all the layers of a image when we don't have access to the Dockerfile)
- docker image inspect [image name]
- docker image save [image name] -o imagename.tar   (this will create a copy of the image, compress it and we can save it locally or share it)
- docker image load -i imagename.tar    (this will load the compressed file to image)
- 