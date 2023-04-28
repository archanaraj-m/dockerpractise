# dockerpractise
* docker commands

docker image build -t <imagename> . 
# -t is tag
docker image ls
docker container run --name <containername> -d -p 3001:5000 <imagename>  
# -d is detached mode, -p is port
docker container ls -a
# -a is all
