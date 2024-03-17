- When we install docker it creates 3 networks automatically.
    1. Bridge
    2. Host
    3. None
- Bridge is the default network a container gets attached to.
- We can specify other network to a container by using command "--network=host/none" during run command.

### Bridge Network
- This is the Private internal network created inside host by docker. All container get attached to this network by default. and they get an internal IP address (usually in 172.17.0.0/16 series)
- The containers can access each other using this internal IP if required.
- To acces any of the container in this Network from outside world we can map the container ports to host port(i.e. -p 80:80).

