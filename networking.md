- When we install docker it creates 3 networks automatically.
    1. Bridge
    2. Host
    3. None
- There are additional networks available when Docker operates in a different mode.
    1. Overlay
    2. IPvLAN
    3. Macvlan
- Bridge is the default network a container gets attached to.
- We can specify other network to a container by using command "--network=host/none" during run command.

### Bridge Network
- This is the Private internal network created inside host by docker. All container get attached to this network by default. and they get an internal IP address (usually in 172.17.0.0/16 series)
- The containers can access each other using this internal IP if required.
- To acces any of the container in this Network from outside world we can map the container ports to host port(i.e. -p 80:80).

### Host Network
- When a container uses host networking, it directly binds to the network interfaces of the Docker host.(i.e. "docker run -d --network host nginx" this commmand will directly publish port 80 to host network)
- It's only available to Linux hosts.
- here we don't need to do additional port binding to host, it directly publishes the port to the host.
- this takes out any network isolation between host network and docker internal network.

### None Network
- In this network the containers are not attached to any network, and doesn't have any access to external network or other containers. They run in a isolated network.

### Overlay Network
- This driver creates a network that spans across multiple Docker hosts, allowing containers on different hosts to communicate with each other. It’s particularly useful for Docker Swarm mode

### IPvLAN Network
- This driver offers precise control over the IPv4 and IPv6 addresses assigned to your containers, as well as layer 2 and 3 VLAN tagging and routing12.

### Macvlan Network 
- This driver allows containers to appear as physical devices on your network by assigning them a MAC address12.

## Custom Network in Docker
- By default docker uses Bridge network and mostly uses 172.17.0.0/16 as default subnet.
- We can create out own network with our own subnet inside docker by using a command i.e
```javascript
    docker network create --driver bridge --subnet 182.18.0.0/16 custom-network-name
```
## Builtin DNS
- Docker have a buildin DNS server which carries the container IPs with container names configured to them.
- The DNS server allways runs at 172.0.0.11
- We can connect Containers to each other just by specifying their names, the builtin DNS server will take care of ip configuring in the backend.



## Commands
- docker network ls
- docker inspect networkname/networkid
- docker network crate --driver driverType --subnet customsub customNetworkName
- docker run -itd --network NetworkName imagename
- docker network connect customNetName containerName   (this will connect a container to a custom network)
- docker network disconnect customNetName containerName
- docker network rm customNetName
- docker network prune   (remove all unused networks)