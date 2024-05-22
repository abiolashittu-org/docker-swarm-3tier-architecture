# Docker Swarm 3-Tier Architecture

![Docker Swarm 3-Tier Architecture](https://github.com/abiolashittu-org/docker-swarm-3tier-architecture/assets/108594160/599ce0eb-4bbc-4476-8ae3-11da6f855e9e)

## Tasks

Using AWS, create a Docker Swarm that consists of one manager and three worker nodes. Verify the cluster is working by deploying the following three-tier architecture:

- A service based on the Redis docker image with 4 replicas.
- A service based on the Apache docker image with 10 replicas.
- A service based on the Postgres docker image with 1 replica.

## Create the Manager Node

1. Navigate your AWS Management Console to EC2, and press ‘Launch Instance’ to create a new EC2 instance.
2. Select Amazon Linux 2 AMI for the instance and choose an instance type. For our project, we will use a `t2.micro`, but depending on your use case, you may want to use a `t2.medium` or an instance with more resources for the manager node. The performance of our swarm cluster may be limited by the resources of the manager node.
3. Configure the rest of the instance details. It is helpful to add a tag for later identification.

### Name and Tags Info

- **Name**: abi-swarm-managenode

![Name and Tags](https://github.com/abiolashittu-org/docker-swarm-3tier-architecture/assets/108594160/f8db72a1-9317-452c-8c48-100f2f113177)

### Launch the Instance

![Launch Instance](https://github.com/abiolashittu-org/docker-swarm-3tier-architecture/assets/108594160/a5f761c5-281a-40bc-a302-884c178d87f1)

We can now connect to our instance via SSH.

![SSH Connection](https://github.com/abiolashittu-org/docker-swarm-3tier-architecture/assets/108594160/416ea2e5-87af-4e11-837a-114b893e32b0)

## Connect to the Instance

We will connect to our instance with the following command which is provided to us:

```bash
ssh -i "abi.pem" ec2-user@325-173-24-20.compute-1.amazonaws.com
```

The above is specific to my project’s instance, but you may fill in the code below with your own instance’s details by following these guidelines:

```bash
ssh -i <path-to-your-private-key-file> <your-username>@<public-ip-address>
```

![SSH Command](https://github.com/abiolashittu-org/docker-swarm-3tier-architecture/assets/108594160/81d1ffa2-544e-4475-9ce6-31d0fcf077cb)

Connect and run any updates requested.

![Update Instance](https://github.com/abiolashittu-org/docker-swarm-3tier-architecture/assets/108594160/d7816a54-1bb6-459f-a20b-395f1c2ee11a)

We are now connected to our instance.

## Install Docker Swarm

Once logged in, we can install Docker Swarm. To do this on Amazon Linux, we will run the following commands:

```bash
sudo yum update -y
sudo amazon-linux-extras install docker -y
sudo service docker start
sudo usermod -aG docker ec2-user
```

![Install Docker](https://github.com/abiolashittu-org/docker-swarm-3tier-architecture/assets/108594160/0aa313f9-301c-4dc2-b96a-500d731e0c1e)

We can then run `docker version` to verify that Docker was successfully installed:

![Verify Docker Installation](https://github.com/abiolashittu-org/docker-swarm-3tier-architecture/assets/108594160/b4b2f747-a48e-4240-b3a2-9432e125b752)

Log out and back in to apply the group membership update:

```bash
exit
ssh -i "abi.pem" ec2-user@325-173-24-20.compute-1.amazonaws.com
```

We are now able to run `docker version` without receiving an error and can verify with `groups` that we are part of the “docker” group.

![Verify Docker Group](https://github.com/abiolashittu-org/docker-swarm-3tier-architecture/assets/108594160/d5f94031-0661-4d2f-a8c8-fd30aee2848a)

![Groups Command](https://github.com/abiolashittu-org/docker-swarm-3tier-architecture/assets/108594160/1472abc4-cd42-4174-a3f2-8c98bb807b88)

## Initialize the Docker Swarm

With Docker installed and correct permissions, we are now able to initialize the Docker Swarm.

First, find the private IP of our instance. We can do this through `ifconfig`:

```bash
ifconfig
```

In this specific project, we already knew our IP because our Amazon EC2 username by default was `ec2-user@325-173-24-20`. However, knowing this command is useful anyway to verify and in case it is not always located in our username.

Now that we have the private IP, we can use it in the command to initialize the Docker Swarm:

```bash
sudo docker swarm init --advertise-addr 325-173-24-20
```

![Initialize Docker Swarm](https://github.com/abiolashittu-org/docker-swarm-3tier-architecture/assets/108594160/0aa313f9-301c-4dc2-b96a-500d731e0c1e)
