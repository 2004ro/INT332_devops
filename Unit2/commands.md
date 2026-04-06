## Essential Docker Commands

**System & Image Management**
* `docker --version` : Check Docker version.
* `docker info` : detailed information.
* `docker images` : List all downloaded images.
* `docker pull <image_name>` : Download an image (e.g., `docker pull ubuntu` or `docker pull python:3.11-slim`).
* `docker push <image_name>` : Upload an image.
* `docker run <new_container_name>` : create and start new container. 
       - -it : run container in interactive mode. allows you to interact with container through command line.
       - -d : runs container in the background. 
       - --name : specifies name for a  container.
       - --rm: automatically removes the container when it exits.
       - -p : maps a host port to a container port.
       - -e/ --env : sets an environment variable inside the container.
       - -v : mounts a host volume inside container.
* `docker run -d httpd` : runs in deatached mode.
* `docker run httpd echo "Hello,World!"` :it runs the container and with argument "Hello,World!"
* `docker run --name my-container httpd echo "Hello,World"` : running container with specific name.
    - --name is used to give name of container.
    - my-container is the name of container.
    - echo is a command
    - "Hello, World" is argument used.
* `docker rmi <username/image>` : Remove a specific image.
* `docker history httpd` : View the layers of an image. (httpd is the image name)

**Container Execution & Management**
* `docker ps` : List currently running containers.
* `docker ps -a` : List all containers (running and stopped).
* `docker run hello-world` : Test if Docker is working.
* `docker run -it ubuntu` : Run an Ubuntu container in interactive mode (`-i` interactive, `-t` terminal).
* `docker run -it --hostname myapp ubuntu bash` : Run a container and assign it a custom hostname.
* `docker run -d -p 8080:80 nginx` : Run Nginx in detached mode (`-d`) and map host port 8080 to container port 80 (`-p`).
* `docker exec <container_id> ls` : Execute a command (like `ls`) inside an already running container.
* `docker logs <container_id>` : Check the logs/output of a specific container.
* `docker run -e MODE=production newapp:v2`
* `docker run -e MY_VAR=value httpd env`: sets an environment variable *MY_VAR* to the value *value* and runs a new container from the *httpd* image. (value can be anything we want)
   - Example:- `docker run -it -e MY_NAME=Bhavini ubuntu bash` : run a container and display the name inside it.
* `docker run -d -e APP_ENV=production -e App_VERSION=1.0 nginx`
   - docker exec -it *container_id* bash
   - echo $APP_ENV
   - echo $APP_VERSION
* For MYSQL
   - `docker run -d -e MYSQL_ROOT_PASSWORD=root123 -e MYSQL_DATABASE=college -e MYSQL_USER=admin -e MYSQL_PASSWORD=admin123 mysql:8`
   - docker exec -it *container_id* bash

* -p optional flag in run command
     - docker run -p <HOST_PORT>:<CONTAINER_PORT> IMAGE 
     - example:- docker run -p 8080:80 nginx

**Basic commands used to create, inspect, verify, delete/remove the volumes**

- docker volume create <volume name> | example : docker volume create mydata
- docker name ls
- docker volume inspect mydata
- docker run -dit -v mydata:/app/data --name contl ubuntu :- attatching the volume(-v mydata:)  and path of data(/app/data)
- docker exec -it contl bash
- echo "Hello Docker Volume" > /app/data/file1.txt
- cat /app/data/file1.txt
- exit
- docker rm -f contl
- docker run -it -v mydata:/app/data ubuntu bash
- cat/app/data/file1.txt
- docker volume rm mydata
- docker volume prune

## Docker network
- docker network ls
- docker run -dit --name c1 nginx
- docker inspect c1|findstr IPaddress
- docker exec -it c1 ping c2

- docker network create mynet
- docker run -dit --name c1 --network mynet busybox
- docker run -dit --name c2 --network mynet busybox
- docker exec -it c1 ping c2

- docker run --network host nginx
- docker run -d --network host nginx 

