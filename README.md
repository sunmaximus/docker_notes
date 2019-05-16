# docker_notes
My own personal notes on how to run docker

# Docker command

```
docker ps
docker ps -a
docker images
```

## SSH into docker Image
This will run once and remove the container. Usually use for debugging the container

`docker run --rm -it node bash`

## create new and rename container 
`docker run --name my-redis -d redis`

## SSH into a Container
`docker exec -it <container name> /bin/bash`

## Build Docker image
`$ docker build -t hello-world .`

## Run the image int he background
Running your image with -d runs the container in detached mode, leaving the container running in the background. The -p flag redirects a public port to a private port inside the container. Run the image you previously built:

`docker run -p 49160:8080 -d <your username>/node-web-app`

# One liner to stop all and remove all container
docker stop $(docker ps -a -q)
docker rm $(docker ps -a -q)


# Node example 
    docker run --name playbook -p 6060:6060 -d snguyen/playbook


## Docker

#### ❗❗❗ Make sure a Dockerfile exist or configured inside the project  

### Helpful Docker Commands
List all docker images:
  
    docker images
List all docker containers:
  
    docker ps -a

Build docker image in directory

    docker build -t <docker name> .

Run docker image with port mapping and custom name

    docker run --name <custom name> -p <host port>:<container exposed port> -d <image name:image tag || imageID >
   
Example:
   
    docker run --name playbook -p 5000:5000 -d react-playbook:2.2.69
   
Docker stop and remove container

    docker stop <container name || container id> 
    docker rm <container name || container id>   

One liner to stop all and remove all container
  
    docker stop $(docker ps -a -q)
    docker rm $(docker ps -a -q)
  
Docker tag and push to repository
    
    docker tag <image id> docker-registrory.com/image-name:tag
    docker push docker-registrory.com/image-name:tag

SSH into docker image without creating a container

    docker run --rm -it <image name:tag> bash
    
SSH into a container

    docker exec -it <container name> /bin/bash
    
Starts a Docker container and configures it to always restart unless it is explicitly stopped or Docker is restarted.

    docker run -dit --restart unless-stopped redis

For the created containers use `docker update` to update restart policy.

    docker update --restart=always 0576df221c0b

Example:
    
    docker tag 27c9559d36ec 10.20.10.122:8083/oracle-database-enterprise-12.2.0.1-slim:100
    docker push 10.20.10.122:8083/oracle-database-enterprise-12.2.0.1-slim:100
