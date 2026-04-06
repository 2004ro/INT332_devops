## Essential Docker Commands

**System & Image Management**
* `docker --version` : Check Docker version.
* `docker info` : detailed information.
* `docker images` : List all downloaded images.
* `docker pull <image_name>` : Download an image (e.g., `docker pull ubuntu` or `docker pull python:3.11-slim`).
* `docker push <image_name>` : Upload an image.
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