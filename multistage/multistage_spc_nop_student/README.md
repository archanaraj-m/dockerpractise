# dockerpractise
Docker Workshop-3 Activities (21/APR/2023) - Khaja Sir   
------------------------------------------------------------------------

1) Create a multi-stage docker file to build  
    a) nop commerce  
    b) spring petclinic
    c) student courses register
## a)nop commerce
* First we can write dockerfile with help of manual commands
* To build this application we need
    dotnet sdk7.0
* Manual steps:
  Download URL = https://github.com/nopSolutions/nopCommerce/releases/download/release-4.60.2/nopCommerce_4.60.2_NoSource_linux_x64.zip
  cd nop 

# Dockerfile
```
FROM ubuntu:22.04 AS extractor
RUN apt update && apt install unzip
ARG DOWNLOAD_URL=https://github.com/nopSolutions/nopCommerce/releases/download/release-4.60.2/nopCommerce_4.60.2_NoSource_linux_x64.zip
ADD ${DOWNLOAD_URL} /nopCommerce/nopCommerce_4.60.2_NoSource_linux_x64.zip
RUN cd /nopCommerce && unzip nopCommerce_4.60.2_NoSource_linux_x64.zip && mkdir bin logs && rm nopCommerce_4.60.2_NoSource_linux_x64.zip


FROM mcr.microsoft.com/dotnet/sdk:7.0
LABEL author="Archana" organization="qt" project="dockerpractis
e"
ARG user=nopcommerce
ARG group=nopcommerce
ARG uid=1000
ARG gid=1000
ARG DOWNLOAD_URL=https://github.com/nopSolutions/nopCommerce/releases/download/release-4.60.2/nopCommerce_4.60.2_NoSource_linux_x64.zip
ARG HOME_DIR=/nop
RUN apt update && apt install unzip -y
# Create user nopcommerce
RUN groupadd -g ${gid} ${group} \
    && useradd -d "$HOME_DIR" -u ${uid} -g ${gid} -m -s /bin/bash ${user}
USER ${user}
WORKDIR ${HOME_DIR}
COPY --from=extractor  /nopCommerce ${HOME_DIR}
EXPOSE 5000
ENV ASPNETCORE_URLS="http://0.0.0.0:5000"
CMD [ "dotnet", "Nop.Web.dll"]

```



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
![preview](./../ms-images/img1.png)
* To check the image
```
  docker image ls
```
* Next create and run the container with this command
  ```
  docker container run --name spccont -d -p 3000:8080 spc
  docker container ps -a
  ```   
![preview](../ms-images/img2.png)
* go to newtab 
* instance public IP address/3001 then spc page came
![preview](../ms-images/img3.png)



1) Push these images to  
    a) AWS ECR
    b) Azure ACR


3) Write a docker compose file for
    a) Nop Commerce
    b) Spring petclinic
    c) Game of life
    d) Student Courses Register
