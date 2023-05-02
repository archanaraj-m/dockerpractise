# dockerpractise
Docker Workshop-3 Activities (21/APR/2023) - Khaja Sir   
------------------------------------------------------------------------
* First we can take one onstance in that install docker with use of this commands(6april2023/directdevops blog)
```
curl -fsSL https://get.docker.com -o get-docker.sh
sh get-docker.sh
```
# 1) Create a multi-stage docker file to build  
    a) nop commerce  
    b) spring petclinic
    c) student courses register
## a)nop commerce

# Let's create a multi-stage docker file to build nop commerce
 * Take an a EC2 Machine and Install Docker by using below commands,
  ```
  curl -fsSL https://get.docker.com -o get-docker.sh
  sh get-docker.sh
  sudo usermod -aG docker ubuntu
  ```
  ![preview](./ms-images/ig1.png)
  After successful installation re-login into your machine
  After re-login try to get docker info
  ![preview](./ms-images/ig2.png)
  ![preview](./ms-images/ig3.png)
  
  ```
  $ docker -—version
  $ docker info
  ```
  ![preview](./ms-images/img8.png)
#  create a dockerfile in vi Dockerfile

* First we can write dockerfile with help of manual commands
* To build this application we need
    dotnet sdk7.0
* Manual steps:
  Download URL = https://github.com/nopSolutions/nopCommerce/releases/download/release-4.60.2/nopCommerce_4.60.2_NoSource_linux_x64.zip
  cd nop 

# Dockerfile
```
FROM ubuntu:22.04 As builder
RUN apt update && apt install unzip -y
ADD https://github.com/nopSolutions/nopCommerce/releases/download/release-4.40.2/nopCommerce_4.40.2_NoSource_linux_x64.zip /nop/nopCommerce_4.40.2_NoSource_linux_x64.zip
RUN cd nop && unzip nopCommerce_4.40.2_NoSource_linux_x64.zip && rm nopCommerce_4.40.2_NoSource_linux_x64.zip
FROM mcr.microsoft.com/dotnet/sdk:7.0
LABEL author="raji" organization="qt" project="learning"
COPY --from=builder /nop /nop-bin
WORKDIR /nop-bin
EXPOSE 5000
CMD [ "dotnet", "Nop.Web.dll", "--urls", "http://0.0.0.0:5000" ]

```
* After creating docker file past it in $ vi dockerfile
* for build the image
```
docker image build -t nopimage .
docker image ls
docker container run --name nopcont -d -p 3001:5000 nopimage
docker container ls -a

```
![preview](./ms-images/img4.png)
* with use of that port number paste in dockerplayground then in newtab nop page came
![preview](./ms-images/img5.png)


## b)spring petclinic
* First we can write dockerfile with help of manual commands
* To build this application we need
    jdk17
    maven
    git
* Manual steps:
  git clone https://github.com/spring-projects/spring-petclinic.git
  cd spring-petclinic 
  mvn package
* that spc file gets created in target/spring-petclinic-*.jar

# Dockerfile
```
FROM alpine/git AS vcs
RUN cd / && git clone https://github.com/spring-projects/spring-petclinic.git && \
    pwd && ls /spring-petclinic

FROM maven:3-amazoncorretto-17 AS builder
COPY --from=vcs /spring-petclinic /spring-petclinic
RUN ls /spring-petclinic 
RUN cd /spring-petclinic && mvn package



FROM amazoncorretto:17-alpine-jdk
LABEL author="archana"
EXPOSE 8080
ARG HOME_DIR=/spc
WORKDIR ${HOME_DIR}
COPY --from=builder /spring-petclinic/target/spring-*.jar ${HOME_DIR}/spring-petclinic.jar
EXPOSE 8080
CMD ["java", "-jar", "spring-petclinic.jar"]
```
* Next copy and paste this dockerfile in our instance(vm) with use of below command
* vi dockerfile
* Next build the image
 ```
   docker image build -t spc .
 ```
![preview](./ms-images/img1.png)
* To check the image
```
  docker image ls
```
* Next create and run the container with this command
  ```
  docker container run --name spccont -d -p 3000:8080 spc
  docker container ps -a
  ```   
![preview](./ms-images/img2.png)
* go to newtab 
* instance public IP address/3001 then spc page came
![preview](./ms-images/img3.png)

## c)student cources register

* First create dockerfile with $ vi dockerfile
```
FROM alpine/git AS vcs
RUN cd / && git clone https://github.com/DevProjectsForDevOps/StudentCoursesRestAPI.git && \
    pwd && ls /StudentCoursesRestAPI

FROM python:3.8.3-alpine As Builder
LABEL author="archana" organization="qt" project="learning"
COPY --from=vcs /StudentCoursesRestAPI /StudentCoursesRestAPI
ARG DIRECTORY=StudentCourses
RUN cd / StudentCoursesRestAPI cp requirements.txt /StudentCourses
ADD . ${DIRECTORY}
EXPOSE 8080
WORKDIR StudentCoursesRestAPI
RUN pip install --upgrade pip
RUN pip install -r requirements.txt
ENTRYPOINT ["python", "app.py"]

```
* Next build the image
```
docker image build -t student .
docker image ls
docker container run --name studentcont -d -p 3000:8080 student
```
![preview](./ms-images/img6.png)
* with use of that port number paste in dockerplayground then in newtab student course register page came
![preview](./ms-images/img7.png)

# push the images to public registry(dockerhub)
* * For spc image (spc repository)
* create a public repository
* goto dockerhub click on create repository
![preview](./ms-images/img11.png)
![preview](./ms-images/img12.png)
* after creating the repository it's came like the below image and that repo name is also like this "<username>/<repositoryname>:tag
* we can give tag (:latest or any based on that image ex: for spc 3.0.0)
![preview](./ms-images/img13.png)
* After building the image tag the image to new naming format
* for that command is ``docker image tag spc archanaraj/myspcimage:3.0.0``
* next ``docker image ls``
* if we give another tag also image is build but image ID not changed only tag will change
* login into docker hub from cli(commandline interface)
* for that docker command is ``docker login``
![preview](./ms-images/img9.png)
* Next push the image to docker hub command is ``docker image push -a archanaraj/myspcimage``
* When we push the same image second time with the diffrent tag it will not create any new image on the docker hub. But it will already layer existed.
* Next show in dockerhub
![preview](./ms-images/img14.png)
* For delete the image command is ``docker image rm <imagename>``
![preview](./ms-images/img15.png)
* * For nop image (nop repository)
* create another public repository for nop
* goto dockerhub click on create repository
![preview](./ms-images/img16.png)
* create nop docker image
* ``docker image ls``
![preview](./ms-images/img17.png)
* After building the image tag the image to new naming format
* for that command is ``docker image tag nop archanaraj/nop:latest``
* next ``docker image ls``
* In the above command tag is given by our wish we can give any in that tag (example ia can give latest,1.0 like,if we can give our name also)
![preview](./ms-images/img18.png)
* login into docker hub from cli(commandline interface)
* for that docker command is ``docker login``
* Next push the image to docker hub command is ``docker image push -a archanaraj/nop``
![preview](./ms-images/img19.png)
* Next show in dockerhub
![preview](./ms-images/img20.png)
* * For student register image (student repository)
* same above process creat the repo in dockerhub
* Next build the image after that create tag for that image 
![preview](./ms-images/img21.png)
* And next login to the docker ``docker login``
* next push the image to dockerhub ``docker image push -a archanaraj/student``
![preview](./ms-images/img22.png)
* check in dockerhub
![preview](./ms-images/img23.png)
# 2) Push these images to  
    a) AWS ECR
    b) Azure ACR
* Private Registries
  There are many applciations for hosting private registries
      AWS: ECR (Elastic container registry)
      Azure: ACR (Azure Container Registry)
      Jfrog  
* First goto AWS => Elastic Container Registry
* In that create repository
![preview](./ms-images/img24.png)
![preview](./ms-images/img25.png)
![preview](./ms-images/img26.png)
* After creating the repository click on that repo we can see =>view push commands
* click on that view push commands 
![preview](./ms-images/img27.png) 
![preview](./ms-images/img28.png)
* Next in the machine install awscli for aws configure 
```
sudo apt update
sudo apt install awscli
aws configure
```
* for aws configure  credentials goto aws=> iam=>users=>add user=>create user=>attach policy AdiministratorAccess
* click on =>Next=>create user=>click on user=>seecurity credentials=>scroll down=> access key=>create access key
![preview](./ms-images/img29.png)
![preview](./ms-images/img30.png)
![preview](./ms-images/img31.png)
* After AWS configure ![preview](./ms-images/img32.png)
* execute the command in that push commands![preview](./ms-images/img28.png)
* execute the command
![preview](./ms-images/img33.png)
![preview](./ms-images/img34.png)
* ckeck in aws elastic container registry(ECR)
![preview](./ms-images/img35.png)
* For pull the image from dockerhub command is ``docker image pull archanaraj/myspcimage:latest``
  ``docker image pull <username/reponame:tag>``
* ``docker image tag archanaraj/myspcimage:latest 760450597737.dkr.ecr.eu-west-3.amazonaws.com/myspcrepo:latest`` in this command create tag for image that 7670........... is created by aws not by us because it's private registry so we can create the tag image with use of it(767.....) 
* For push the image to ECR repo command is ``docker image push 760450597737.dkr.ecr.eu-west-3.amazonaws.com/myspcrepo:latest``
  ``docker image push <image name with tag>``
![preview](./ms-images/img36.png)

1) Write a docker compose file for
    a) Nop Commerce
    b) Spring petclinic
    c) Game of life
    d) Student Courses Register
