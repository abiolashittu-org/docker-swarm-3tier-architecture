## docker-swarm-3tier-architecture

![image](https://github.com/abiolashittu-org/docker-swarm-3tier-architecture/assets/108594160/599ce0eb-4bbc-4476-8ae3-11da6f855e9e)

Tasks
Using AWS, create a Docker Swarm that consists of one manager and three worker nodes.
Verify the cluster is working by deploying the following three tier architecture:
- a service based on the Redis docker image with 4 replicas
- a service based on the Apache docker image with 10 replicas
- a service based on the Postgres docker image with 1 replica

Create the Manager node
Navigate your AWS Management Console to EC2, and press ‘Launch Instance’ to create a new EC2 instance. Select Amazon Linux 2 AMI for the instance and choose an instance type. For our project, we will use a t2.micro, but depending on your use case you may want to use a t2.medium or an instance with more resources for the manager node. The performance of our swarm cluster may be limited by the resources of the manager node.
Configure the rest of the instance details. It is helpful to add a tag as well for later identification.

Name and tags info
name
