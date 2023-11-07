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
5. started mongo with some options. see mongodb.txt
6. docker logs mongodb: {"t":{"$date":"2023-11-06T00:55:18.339+00:00"},"s":"I",  "c":"NETWORK",  "id":23016,   "ctx":"listener","msg":"Waiting for connections","attr":{"port":27017,"ssl":"off"}}
7. stated mongo-express with some options. mongo-express.txt
8. logged in localhost:8081 and created db user-account
9. pulled https://gitlab.com/twn-devops-bootcamp/latest/07-docker/js-app
10. performed steps to end on localhost:3000, edited data and saw on DB the new entries


--------------------------------------------------

Running multiple serivces with docker compose
1. created mongo-compose.yml
2. start container with docker-compose -f mongo-compose.yml up -d
3. stop container with docker-compose -f mongo-compose.yml down

--------------------------------------------------

Dockerfile - Build own docker image
1. created dockerfile.
2. docker build -t my-app:1.0 . (location of dockerfile)
3. result: Successfully tagged my-app:1.0
4. updated dockerfile with workdir and RUN npm install
5. build image docker build -t js-app:1.0 .
6. docker run js-app:1.0 Result: app listening on port 3000

--------------------------------------------------

Private Docker Repo
1. pushed and pulled from aws repo. pulled with updated mongo-compose.yml

--------------------------------------------------

Docker Volumes
1. watched video, skipped working on it as i'm using docker in my private homelab.
2. example of jellyfin container volumes in ansible playbook:
  - name: Deploy jellyfin
    community.docker.docker_container:
      name: jellyfin
      image: jellyfin/jellyfin
      state: started
      restart_policy: unless-stopped
      volumes:
        - /mnt/server/docker/jellyfin/cache:/cache
        - /mnt/server/docker/jellyfin/config:/config
        - /mnt/server/media:/media
      network_mode: host
3. Updated mongo-compose.yml with local volumes


--------------------------------------------------

Create docker hosted repo on nexus
1. created repo named docker-hosted
2. created role with priviliges view-docker-hosted*
3. added port http 8083 for repo, also opened in FW
4. added docker bearer token realm
5. edited docker.json to allow http repos
6. logged in with docker login
7. build app again and retagged it with nexus IP:port
8. pushed with docker push IP:port/js-app:1.0


--------------------------------------------------

Deploy Nexus as Docker Container
1. deployed a new VM locally on my proxmoxhost using terraform
2. configured new host with ansible. please see nexus.yml
3. tasks include to install docker, mount nfs volumes and start and deploy nexus. Please see nexus-task.yml
4. ran playbook, cat adminpassword and ran wizard after first start


--------------------------------------------------

Reference: DevOps Bootcamp and TWN