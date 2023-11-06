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
1. docker logs -f id or name (-f to see new logs if container is running)
2. docker stop $(docker ps -a -q) (Just for me, stopps all containers)
3. docker run --name redis (will name the container redis, easier to remember)
4. docker exec -it id or name /bin/sh (get terminal inside of the container with root user)
5. inside a container you may miss some applications like curl. Container just have needed application to function (much more safety and light weight)
6. docker run with its options creates the container. docker start and stop are interacting with already created containers

--------------------------------------------------

Docker demo project
1. docker pull mongo && docker pull mongo-express
2. docker network ls (lists docker networks)
3. created a docker network with docker network create mongo-network
4. pulled mongo and mongo-express
5. started mongo with some options:
docker run -d \
-p 27017:27017 \
--name mongodb \
--network mongo-network \
-e MONGO_INITDB_ROOT_USERNAME=admin \
-e MONGO_INITDB_ROOT_PASSWORD="password" \
mongo
6. docker logs mongodb: {"t":{"$date":"2023-11-06T00:55:18.339+00:00"},"s":"I",  "c":"NETWORK",  "id":23016,   "ctx":"listener","msg":"Waiting for connections","attr":{"port":27017,"ssl":"off"}}
7. stated mongo-express with some options:
docker run -d \
-p 8081:8081 \
--name mongo-express \
--network mongo-network \
-e ME_CONFIG_MONGODB_ADMINUSERNAME=admin \
-e ME_CONFIG_MONGODB_ADMINPASSWORD="password" \
-e ME_CONFIG_MONGODB_SERVER=mongodb \
-e ME_CONFIG_BASICAUTH_USERNAME=admin \          
-e ME_CONFIG_BASICAUTH_PASSWORD="password" \
mongo-express
8. logged in localhost:8081 and created db user-account
9. pulled [the ](https://gitlab.com/twn-devops-bootcamp/latest/07-docker/js-app)https://gitlab.com/twn-devops-bootcamp/latest/07-docker/js-app
10. performed steps to end on localhost:3000, edited data and saw on DB the new entries
