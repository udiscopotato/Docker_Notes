


Features of Docker Swarm:
- Simplified Setup
- Declarative
- Scaling
- Rolling Update
- Self Healing
- Security
- Load Balancing
- Service Discovery

## Setup
- Docker engine comes with Swarm by default, but stays in inactive state unless it's activated manually.
- we can check a node is part of a cluster or not by checking "docker system info" command. if it shows swarm as active this means it is connected or is a part of swarm cluster.
- to initiate swarm we need to follow some pre-requisite i.e:
OPEN REQUIRED PORTS
1. TCP 2377  (Cluster Management Communication)
2. TCP & UDP 7946   (Communication among Nodes)
3. UDP 4789   (Overlay Network)
- After this we need to install Docker enginer on every nodes.
- After this we need to run "docker swarm init" command on Manager node. It'll give a specific command to run on worker nodes with token.
- Run the the command "docker swarm join --token "token by manager" ManagerIP:2377 on worker nodes.

## Service

## Commands
- docker system info
- docker swarm init
- docker swarm join --token [token by Master NOde initialization] MASTERIP:2377
- docker node ls
- docker swarm join-token worker
- docker node inspect [node name] --pretty
- docker node promote [node name]
- docker node demote [node name]
- docker node update --availability drain [node name]
- docker node update --availability active [node name]
- docker swarm leave
- docker node rm [node name]
- docker service create --replicas 3 nginx
- docker service create --name serviceName -p pcPort:contPort nginx:alpine
- docker service ls
- docker service ps serviceName
- docker service inspect serviceName --pretty
- docker service update --replicas 5 -p pcPort:contPort serviceName
- docker service update -p pcPort:contPort --image newImage serviceName  (Rolling Update)
- 
