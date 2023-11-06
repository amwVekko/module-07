# module-07
Containers with Docker


Main docker commands
1. docker pull redis (downloads latest image)
2. docker images (shows info about the images, like tag, size)
3. to start a container docker run -d redis (detach mode)
4. docker ps -a (lists all containers, with state, ports etc. also stopped containers if needed to restart them)
5. docker stop id or name of the container
6. docker pull redis:6.2 (will pull the specific version)
7. if two containers using the same port you need to specify the port used on the host the container is running e.g. docker run -d -p 6000:6379 redis

-----------------------------------------------------

Debug commands
