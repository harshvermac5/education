# Types of communication between containers

1. Bridge network (Default) 
2. Host network (acts like running an application rather than container)
3. None
4. Docker IP VLAN network (mirror mode, present as new device over the network, although MAC address remains the same)
5. MAC VLAN network
6. Overlay network


# Notes:
- Docker ports need to be forwarded in mac (localhost), unlike linux which can be accessed directly.- DNS is not supported in default bridge mode
- Docket compose file is used to list multiple container and its respective network in a single place
- `-f` stands for file and `-d` stands for detached (background) in context of running docker
- Host network provides no network isolation, and only works on linux though.
- Overlay networks provides connectivity between multiple swarm of containers, it works on principle of manager and worker nodes.
- bridges are automatically created for worker nodes once they run a container with the required bridge.

Three tier application model:
1. Presentation tier (client like web-browser, app)
2. Logic tier (API handling calculations)
3. Data tier (Storage services)

# Commands

- `docker network ls` lists all the networks.
- `docker network inspect bridge` lists details about specific network (bridge in this case).
- `docker ps` lists all the running containers.
- `docket inspect <container-name>` list all the details about a specific container.
- `curl localhost:<exposed-port>/api/info` shows the hostname and ip of the container.
- `docker network create <bridge-name> --subnet 10.0.0.0/19 --gateway 10.0.0.1` creates a new bridgewith specified parameters.
- `docker run -d --name <container-name> -p <host-pport>:<container-port> --network <bridge-name>` runs the container with specified bridge.
- `docker compose -f <compose-file.yaml> up -d` launches all the application and initiates the mentioned bridge in the file.
- `docker run -d --name <container-name> --network host` runs the container with host network configured.
- `docker network create -d ipvlan --subnet=192.168.50.0/24 --gateway=192.168.50.1 -o ipvlan_mode=l2 -o parent=<interface-name> <bridge-name>` creates a docker IP VLAN bridge.
- `docker network create -d macvlan --subnet=192.168.50.0/24 --gateway=192.168.50.1 -o parent=<interface-name> <bridge-name>` creates a MAC VLAN bridge.
- `sudo ethtool -K <interface-name> tx-checksum-ip-generic off` turns off the problematic interface in case of overlay network
- `docker swarm init` generates a token to connect with worker node, the output command to be pasted in worker node to join the swarm 
- `docker network create -d overlay --attachable <bridge-name>
