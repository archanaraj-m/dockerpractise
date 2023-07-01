# dockerpractise
* docker commands

docker image build -t <imagename> . 
# -t is tag
docker image ls
docker container run --name <containername> -d -p 3001:5000 <imagename>  
# -d is detached mode, -p is port
docker container ls -a
# -a is all

# Building Docker Images
* Docker image is required to create container.
* Docker images are OCI compliant i.e. they can be executed in other container runtimes as well
* Docker image will have all the necessary contents to run an application
* We need to build docker images to run our application inside container. This process is called as "Containerization"
# To Build docker images we have 3 ways
* Start from scratch and add components file by file
* Create a container with some image, make changes to run your application and create a image from the running contianer (commit)
* Using a file with all the instructions to create image (Dockerfile)
Creating images from scratch
* Docker has a reserved image (base-image) that is is empty & is known as scratch
* Even os components which are necessary to start the main process in container has to be copied by us
* Creating Images interactively
Game of life
[ReferHere](https://referenceapplicationskhaja.s3.us-west-2.amazonaws.com/gameoflife.war) for the war file
To run this application we need tomcat 8 or 9 with jdk 8 installed
Copy the war file into webapps folder
```
sudo apt update
sudo apt install openjdk-8-jdk tomcat9 -y
```
Create a container in an interactive way or detached mode
```
docker container run -d -p 37000:8080 --name gol tomcat:9-jdk8
docker container exec -it gol /bin/bash
cd webapps
wget https://referenceapplicationskhaja.s3.us-west-2.amazonaws.com/gameoflife.war
# now access the application over http://<ip-docker-host>:37000/gameoflife
```