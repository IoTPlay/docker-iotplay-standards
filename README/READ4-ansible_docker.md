# Ansible for docker

---> Back to the README file with the [Table of Contents](../README.md).

## 1. ansible-container General

- Instructions [ansible-container](https://docs.ansible.com/ansible-container/installation.html)
- Installing `sudo -H pip install ansible-container[docker]`
- Using ansible-container to build your next application base image: [codementor blog](https://www.codementor.io/slavko/using-ansible-container-to-build-your-next-application-base-image-c4eq2ise1)

- docker containers: [module](http://docs.ansible.com/ansible/latest/docker_container_module.html)
- When running ansible playbook for docker_images, and you get `unauthorized: incorrect username or password`, then `docker login`

### Ansible Docker Swarms (does not work...)

Blog for Docker Swarm in Ansible: [Docker Swarm blog](https://thisendout.com/2016/09/13/deploying-docker-swarm-with-ansible/), with files here: [github](https://github.com/nextrevision/ansible-swarm-playbook)

- Determine the status of the swarm cluster
- Optionally bootstrap a cluster
- Retrieve the join tokens
- Join manager nodes
- Join worker nodes

### Ansible Docker issues


## Swarm support
- Ansible does not support swarm, or stack mode yet. (Dec'17)  
  - a work around is to deploy a docker-compose which has the swarm def in it. [roles for docker swarm](https://github.com/atosatto/ansible-dockerswarm)
  - And, understanding the stack: [jmkael docker stack blog](http://jmkhael.io/deploy-swarm-services-with-the-new-docker-stack-and-a-compose-file-2/)
  - I have issues with local host, solution: [github issue](https://github.com/ansible/ansible/issues/33132)  


- ansible "msg": "Error starting project UnixHTTPConnectionPool(host='localhost', port=None): Read timed out. (read timeout=60)"}   
  - Same issue, solution [github](https://github.com/ansible/ansible-container/issues/147). Do this on docker host:
    > export DOCKER_CLIENT_TIMEOUT=500   
      export COMPOSE_HTTP_TIMEOUT=500  

  - Also try `export ANSIBLE_CONFIG="/your/folder/location"`

----------------
## Ansible in a CONTAINER

Instructions on installing Ansible Container [docs.ansible](https://docs.ansible.com/ansible-container/installation.html#getting-ansible-container)

- `sudo pip install ansible-container[docker]`  
- `cd /tmp`  
- `git clone https://github.com/ansible/ansible-container.git`  
- `cd ansible-container`  
- `sudo -H pip install -e .[docker]`  
- `sudo -H pip install --upgrade setuptools`  
- In a new project folder, `ansible-container init`  

#### Managing Docker Containers with ansible

- Managing Docker Containers with Ansible: [Linux Acadeny](https://linuxacademy.com/howtoguides/posts/show/topic/13750-managing-docker-containers-with-ansible)

#### Other ansible-container subcommands enable the container development workflow:

- The Containers in the yml, must be under a services section for it to work.  
- In the container.yml, you can use:  
> dev_overrides:  
      environment:  
        - "DEBUG=1"  

- The files to configure:
  - `meta.yml`: if you want to upload your project to Galaxy.
  - [ansible-requirements.yml](https://docs.ansible.com/ansible-container/getting_started.html#ansible-requirements-txt) - any python deps?
  - If the roles in your container.yml file are in Ansible Galaxy or a remote SCM repository, and your project depends upon them, add them to `requirements.yml`.

#### How to make it work  

- [docs.ansible](https://docs.ansible.com/ansible-container/getting_started.html#dipping-a-toe-in-starting-from-scratch):  

#### Commands you can run with it
- `ansible-container build` initiates the build process. It builds and launches the Conductor Container. The Conductor then runs instances of your base container images as specified in container.yml. The Conductor container applies Ansible roles against them, committing each role as new image layers. Ansible communicates with the other containers through the container engine, not through SSH.  
- `ansible-container run` orchestrates containers from your built images together as described by the container.yml file. The container.yml can specify overrides to make development faster without having to rebuild images for every code change.  
- `ansible-container deploy` uploads your built images to a container registry of your choice and generates an Ansible playbook to orchestrate containers from your built images in production container platforms, like Kubernetes or Red Hat OpenShift.


#### Other Instructions

- Create own conductor: [Conductor Container creation](https://docs.ansible.com/ansible-container/conductor.html#baking-your-own-conductor-base)


- Docker Registry - pushing images:  [docs.ansible](https://docs.ansible.com/ansible-container/registry_auth.html#pushing-images)

---> Back to the README file with the [Table of Contents](../README.md).
