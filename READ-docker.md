## General docker help & ToDo's
The ONE readme for docker todo's - move around in folders, keep one, eventually place somewhere central.

##### Instructions to Run a Container:
Containers can be run, but rather do the next step - the docker-compose.yaml route.

1. Image to a Container:  
`docker run -d --name paradoxip  iotplay/python_paradox`
1. Check if it started successfully:
 * `docker ps -a` - get the containerID
 * `docker logs -f <containerID>` to get the logs, running or dead container

##### General HowTo's
- Daily pruning of the docker system: `docker system prune -f`
- To see how the Docker daemons are getting started: `ansible all -m shell -a "pgrep -a docker" `
- To claim some disk space back: `ansible all -m shell -a "docker system prune --all --force"  `

##### Docker Images
- Multi-architecture images, using the manifests tool [container solutions blog](http://container-solutions.com/multi-arch-docker-images/)

- Create and share first image [deis blog](https://deis.com/blog/2015/creating-sharing-first-docker-image/):
  - $ docker build -f Dockerfile -t image_name:tag .

###### Docker Inspect (image)  
Command examples:  
- `docker inspect --format='{{json .Config}}' imageid`  
- `docker inspect --format='{{json .Architecture}}' imageid`  
- `docker inspect --format='{{json .ContainerConfig}}' imageid`  
- `docker inspect --format='{{json .ContainerConfig.Labels}}' imageid`  

##### Docker Containers
- Stop a container: `docker stop -containerid-`  
- List all containers: `docker ps -a`  
- Remove container: `docker rm -containerid-`  

##### About Docker services  
- List Docker Services:  `docker service ls`  
- Check if a swarm is active: `docker info | grep Swarm`  
- Docker swarm nodes: `docker node ls`  
- Docker swarm init: `docker swarm init on -hostname-`  
- Docker swarm leave: `docker swarm leave --force `  
- Docker services stats: `docker stats --all --format 'table {{.Name}}\t{{.CPUPerc}}\t{{.MemUsage}}\t{{.MemPerc}}'`  

##### About Docker-compose
- Difference between ports and expose:  [stackoverflow](https://stackoverflow.com/questions/40801772/what-is-the-difference-between-docker-compose-ports-vs-expose)  

##### Docker Secrets

- Blog on secrets [scottlogic](http://blog.scottlogic.com/2017/03/01/docker-secrets.html)  
- Docker secrets with swarm:   [stackoverflow](https://stackoverflow.com/questions/42139605/how-do-you-manage-secret-values-with-docker-compose-v3-1)  
- blog [codeship](https://blog.codeship.com/docker-secrets-management/)

##### Docker Registry  

###### Private Registry

####### Used docker Images
- We used this one.  budry/registry-arm [docker hub](https://hub.docker.com/r/budry/registry-arm/)
- Docker Image `docker/docker-registry`, but we did not use this one, could not get it to work.
[docker-registry](https://github.com/docker/docker-registry/blob/master/README.md)  

####### Nice infos & blogs:  

- [stack overflow](https://stackoverflow.com/questions/26026931/setting-up-a-remote-private-docker-registry)  
- Official [docs.docker](https://docs.docker.com/registry/deploying/#basic-configuration) with commands like (see the link):  
  - Start the registry automatically  
  - Customize the storage location  
  - Run an externally-accessible registry  
  - Run the registry as a (swarm) service  
  - Native basic auth  
- Listing Repos blog   [docs.docker](https://docs.docker.com/v1.8/registry/spec/api/#listing-repositories)  


- Commands:  
  - $ docker tag ubuntu:16.04 localhost:5000/my-ubuntu  
  - $ docker push localhost:5000/my-ubuntu  
  - $ docker image remove ubuntu:16.04  
  - $ docker pull localhost:5000/my-ubuntu  
  - listing repos `curl http://192.168.1.33:5000/v2/_catalog`
  - $ docker stop registry  
  - Now stop your registry and remove all data
    > docker stop -registry-container- && docker rm -v registry

###### Docker Cloud registry

- docker blog: [docs.docker](https://docs.docker.com/docker-cloud/builds/push-images/)  

  - export DOCKER_ID_USER="iotplay"  
  - docker login
  - docker tag my_image $DOCKER_ID_USER/my_image
  - docker push $DOCKER_ID_USER/my_image




#### Sources
- Clean up docker [yohanlinyanage blog](http://blog.yohanliyanage.com/2015/05/docker-clean-up-after-yourself/)
