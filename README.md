# How you run docker agent
* Docker client to send metric to graphite backend. I have build docker agent to docker image. You can configure your own graphite server info.
* I use docker-compose to run docker agent on docker host and send metric to graphite (cpu, ram, total read, write disk and total tranfer, receiver bytes network)
* Docker-compose.yml file
```
* install docker-compose
pip install docker-compose

* Create docker-compose file
version: '2'
services:
  docker-monitor-agent_1:
    image: lamhaison/docker-agent:v1.12.3_interval
    restart: always
    network_mode: "host"
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
    container_name: "docker-agent_node1"
    environment:
      - GRAPHITE_SERVER=your_server_ip
      - GRAPHITE_PORT=2003
      - PREFIX=docker
      # interval 5s
      - INTERVAL=5000      
* Run docker agent
docker-compose -f docker-compose.yml up -d
```



# Graph on grafana
![alt tag](https://github.com/lamhaison/docker-monitor-agent/blob/master/Screen%20Shot%202017-09-17%20at%201.25.47%20AM.png)
![alt tag](https://github.com/lamhaison/docker-monitor-agent/blob/master/Screen%20Shot%202017-09-17%20at%201.27.24%20AM.png)



# How to create graphite server, please head of [how to setup graphite server](https://github.com/nickstenning/docker-graphite)
