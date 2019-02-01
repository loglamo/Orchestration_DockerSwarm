# <b>Basic Docker Swarm</b>
## Docker Swarm is one of lots of technologies for Orchestartion such as: Docker Swarm, Kubernetes, Apache Mesos, ...
## This document pays attention to basic manipulations to make a Docker Swarm
## <b> 1. Create a Swarm</b>

To create a swarm, first of all, you should create some nodes (Machines), one is manager node, the last ones are workers. You can make a node with:

      docker-machine create []
      docker-machine ls # the list of nodes you have
      docker-machine rm [name of machine] # remove a machine

More information at [Docker-machine create](https://docs.docker.com/machine/reference/create/)

After creating nodes, you can ssh to nodes and work as you like. Nodes are VMs, now. 

You ssh to node you want it to be the manager, and init a swarm with:

       docker swarm init [Ip:port]

After initting a Swarm, you can ssh to workers to add them to Swarm with:

       docker swarm join []

Nodes can join as workers or managers. More information at [Docker Swarm join](https://docs.docker.com/engine/reference/commandline/swarm_join/).
You should set up the manager and workers at different ports.

## <b>2. Create a service</b>

After creating a swarm, you can create a service on it or schedule our containers on it. All we are going to do is tell the manager to run the containers for us and it will take care of scheduling out the containers, sending the commands to the nodes and distributing it.

Something you need to have is:
- What Docker image you want to run to make your app.
- Which port you want to expose your service at.
- The number of containers (or instances) you want to launch (Via replicas parameter)
- The name of your service

You can use:

      docker service create --replicas [replicas] -p p:p --name [name of service]  [the name of image]
      docker service ls # the list of services you have
      docker service ps [name of service] #to see the containers running in service

You can access the service through Ip of machine: http://[machine-ip] in the browser. 
You can scale up and down with:
      
      docker service scale [the name of service]=n

Inspect the node with:

      docker node inspect [the name of node]

Remove the service:

     docker service rm [the name of service]

Update image:

     docker service update --image <the name of image>:<version> [the name of service]

The above information is about how to build a basic Swarm with VMs.
The next document is about how to deploy Swarm on Google Compute Engine(GCE).

# the end. 