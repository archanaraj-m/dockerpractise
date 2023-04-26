## Interview Questions
* 1.what directives we use in docker so far?
  LABEL,RUN,WORKDIR,EXPOSE,ENV,ADD,COPY,
* 2.what is the entrypoint?
  Docker entrypoint is a Dockerfile directive or instruction that is used to specify the executable which should run when a container is started from a Docker image. It has two forms, the first one is the ‘exec’ form and the second one is the ‘shell’ form. If there is no entrypoint or CMD specified in the Docker image, it starts and exits at the same time that means container stops automatically so, we must have to specify entrypoint or CMD so that when we will start the container it should execute something rather than going to stop.
* 3.Before FROM any directive we use?
  ARCH
* 4.which directive we can use for taking dockerfile?
  FROM
* 5.difference between ARG and ENV directives in docker?
ENV is for future running containers. ARG for building your Docker image. ENV is mainly meant to provide default values for your future environment variables. Running dockerized applications can access environment variables. It’s a great way to pass configuration values to your project. ARG values are not available after the image is built.
* 6.What is milithone?
  All of done in one server i.e milithone
* 7.what is the use of this command "docker exec -it <containername/id> /sh
* It is used for inside the container and /sh is for alpine image and /bin/sh is used for ubuntu. 
* 8.what is docker?
* Docker is an open platform for developing, shipping, and running applications. Docker enables you to separate your applications from your infrastructure so you can deliver software quickly. With Docker, you can manage your infrastructure in the same ways you manage your applications. By taking advantage of Docker’s methodologies for shipping, testing, and deploying code quickly, you can significantly reduce the delay between writing code and running it in production.


## Kubernetes Questions

# distributed system kubernetes:
Kubernetes provides you with a framework to run distributed systems resiliently. It takes care of scaling and failover for your application, provides deployment patterns, and more. For example: Kubernetes can easily manage a canary deployment for your system.
# node:
A Kubernetes node is a machine that runs containerized workloads as part of a Kubernetes cluster. A node can be a physical machine or a virtual machine, and can be hosted on-premises or in the cloud. A Kubernetes cluster can have a large number of nodes—recent versions support up to 5,000 nodes.
# Cluster Kubernetes:
What is a Kubernetes cluster? A Kubernetes cluster is a set of nodes that run containerized applications. Containerizing applications packages an app with its dependences and some necessary services. They are more lightweight and flexible than virtual machines.
# What are the states in Kubernetes?
There are three possible container states: Waiting , Running , and Terminated . To check the state of a Pod's containers, you can use kubectl describe pod <name-of-pod> .
# What is stateful and stateless application in Kubernetes?
Stored Data: If the webserver stores data in a backend manner and uses it to identify the user as an always-connected client, the service is Stateful. While in Stateless, the server does store data, but in a database to verify user/client whenever it needs to connect.
# What does monolithic mean in Kubernetes?
Similarly, a monolithic architecture suggests a single-tiered application where all different components from a single platform can be combined and used for a single program.
# why we use odd number nodes in kubernetes?
In order to facilitate availability of master services, they should be deployed with odd numbers (e.g. 3,5,7,9 etc.) so quorum (master node majority) can be maintained should one or more masters fail.
