Interview questions
--------------------
1.Tell us about yourself?

# 2.Explain Docker Images?
* A Docker image is a file used to execute code in a Docker container. Docker images act as a set of instructions to build a Docker container, like a template. Docker images also act as the starting point when using Docker. An image is comparable to a snapshot in virtual machine (VM) environments.

Docker is used to create, run and deploy applications in containers. A Docker image contains application code, libraries, tools, dependencies and other files needed to make an application run. When a user runs an image, it can become one or many instances of a container.

Docker images have multiple layers, each one originates from the previous layer but is different from it. The layers speed up Docker builds while increasing reusability and decreasing disk use. Image layers are also read-only files. Once a container is created, a writable layer is added on top of the unchangeable images, allowing a user to make changes.
[Referhere](https://www.techtarget.com/searchitoperations/definition/Docker-image)

# 3.What are different ways of building docker images?
* [Referhere](https://medium.com/bb-tutorials-and-thoughts/docker-three-ways-to-create-container-images-and-their-use-cases-ee651c0aceef)
* Three ways of Building Images
There are three ways to create container images while working with docker. Let’s explore these methods

        1.Interactively building Images
        2.Using Dockerfile
        3.Importing from a tarball

# 4.What is Dockerfile?
* Dockerfile: [Referhere](https://www.simplilearn.com/tutorials/docker-tutorial/what-is-dockerfile)
Dockerfile is a simple text file that consists of instructions to build Docker images.Dockerfile is a text document containing all the commands the user requires to call on the command line to assemble an image. With the help of a Dockerfile, users can create an automated build that executes several command-line instructions in succession.
* Using Dockerfile
This is a common method to create images in production or testing. Most of the time we use this method

# 5.How is container different than VM?
* [Referhere](https://learn.microsoft.com/en-us/virtualization/windowscontainers/about/containers-vs-vm)
* 
6.Can you tell something about namespaces and how they are used in Docker?
* Docker uses a technology called namespaces to provide the isolated workspace called the container. When you run a container, Docker creates a set of namespaces for that container. These namespaces provide a layer of isolation. Each aspect of a container runs in a separate namespace and its access is limited to that namespace.

# 7.What is difference between ADD and COPY Instruction?
* COPY is a docker file command that copies files from a local source location to a destination in the Docker container. ADD command is used to copy files/directories into a Docker.
* ADD and COPY are two similar Dockerfile instructions which let you add content to your images at build time. Whereas COPY is a straightforward source to destination copy, ADD includes extra functionality for working with archives and remote URLs.

# 8.Can you explain the concept of Layers in Docker Image?
[Referhere](https://dzone.com/articles/docker-layers-explained)

# 9.What is the purpose of EXPOSE and VOLUME instruction in Dockerfile?

# 10.What is your workflow for CI/CD with Docker Containers and where do you store images?
* A version control system (VCS) is a unified source code repository that maintains code changes. This generates the trigger for a CI/CD tool to start the pipeline whenever a new change is pushed into its repository. Image registries store the Docker container images.
* [Referhere](https://r.search.yahoo.com/_ylt=AwrKDx7QXklkSVoSXT27HAx.;_ylu=Y29sbwNzZzMEcG9zAzIEdnRpZAMEc2VjA3Nj/RV=2/RE=1682558801/RO=10/RU=https%3a%2f%2fthenewstack.io%2fkubernetes-ci-cd-pipelines-explained%2f%23%3a~%3atext%3dA%2520version%2520control%2520system%2520%2528VCS%2529%2520is%2520a%2520unified%2crepository.%2520Image%2520registries%2520store%2520the%2520Docker%2520container%2520images./RK=2/RS=a4ir6Nai51EN_DLj5b50i809ZbA-)