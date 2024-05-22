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
name abi-swarm-managenode

![image](https://github.com/abiolashittu-org/docker-swarm-3tier-architecture/assets/108594160/f8db72a1-9317-452c-8c48-100f2f113177)
##Launch the instance
![image](https://github.com/abiolashittu-org/docker-swarm-3tier-architecture/assets/108594160/a5f761c5-281a-40bc-a302-884c178d87f1)

We can now connect to our instance via SSH.

![image](https://github.com/abiolashittu-org/docker-swarm-3tier-architecture/assets/108594160/416ea2e5-87af-4e11-837a-
114b893e32b0)

##We will connect to our instance with the following command which is provided to us:
ssh -i "abi.pem" ec2-user-325-173-24-200.compute-1.amazon.com

The above is specific to my project’s instance, but you may fill in the code below with your own instance’s details by following these guidelines:

ssh -i <path-to-your-private-key-file> <your-username>@<public-ip-address>

![image](https://github.com/abiolashittu-org/docker-swarm-3tier-architecture/assets/108594160/81d1ffa2-544e-4475-9ce6-31d0fcf077cb)






