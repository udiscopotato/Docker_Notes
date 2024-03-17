Components of Docker:
    1. Docker Client
    2. Docker RestAPI
    3. Docker Engine
        - Docker Daemon
            - ContainerD
                - RunC

### Docker Client and Docker Enginer can be in same or different system. to use docker enginer from another system we can change configuration files. of
1. export DOCKER_HOST="tcp://192.168.1.32:2375"
    then: dockerd --debug --host=tcp://192.168.1.32:2375
2. add file at /etc/docker/daemon.json
    ```javascript
        {
            "debug": true,
            "hosts": ["tcp://192.168.1.32:2376"]
            "tls": true,
            "tlscert": "/var/docker/server.pem",
            "tlskey": "/var/docker/serverkey.pem"
        }
    ```
    For unencrypted transmission port: 2375
    For encrypted transmission port: 2376
