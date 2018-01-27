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
