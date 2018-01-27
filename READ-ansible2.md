# General Ansible HowTo & Tips. Dealing with Errors

This general howto and tips to be moved to a central folder, move it around as we work.

## Insanely Complete playbooks

- Commented playbook [github phred](https://gist.github.com/phred/2897937)

## General tips and tricks

- To get the version of ansible, which cfg, and which hosts file: `ansible --version`
- Different env variables per task:
  - Setting per Task only: [stackoverflow](https://stackoverflow.com/questions/27733511/how-to-set-linux-environment-variables-with-ansible)
  - [examples](https://github.com/ansible/ansible-examples/blob/master/language_features/environment.yml)
  - [another one](https://gist.github.com/davejamesmiller/44e5c418c8a3b5f691a64d83fbdbe3d1)
- Dealing with localhost: [tricks of the trade blog](http://www.tricksofthetrades.net/2017/10/02/ansible-local-playbooks/) and [pickle blog](http://ansible.pickle.io/post/86598332429/running-ansible-playbook-in-localhost)
  - sudo vim /etc/ansible/hosts
  - what worked, put the following in the playbook:
     - hosts: 127.0.0.1  
        connection: local


### Only running subset of tasks in a Playbook

> tasks:

> ```
> - yum: name={{ item }} state=installed
>   with_items:
>      - httpd
>      - memcached
>   tags:
>      - packages
> - template: src=templates/src.j2 dest=/etc/foo.conf
>   tags:
>      - configuration
> ```

`ansible-playbook example.yml --tags "configuration,packages"`

## Ansible for docker

- docker containers: [module](http://docs.ansible.com/ansible/latest/docker_container_module.html)
- When running ansible playbook for docker_images, and you get `unauthorized: incorrect username or password`, then `docker login`

#### Ansible Docker Swarms (does not work...)

Blog for Docker Swarm in Ansible: [Docker Swarm blog](https://thisendout.com/2016/09/13/deploying-docker-swarm-with-ansible/), with files here: [github](https://github.com/nextrevision/ansible-swarm-playbook)

- Determine the status of the swarm cluster
- Optionally bootstrap a cluster
- Retrieve the join tokens
- Join manager nodes
- Join worker nodes

#### Ansible Docker issues


##### Swarm support
- Ansible does not support swarm, or stack mode yet. (Dec'17)  
  - a work around is to deploy a docker-compose which has the swarm def in it. [roles for docker swarm](https://github.com/atosatto/ansible-dockerswarm)
  - And, understanding the stack: [jmkael docker stack blog](http://jmkhael.io/deploy-swarm-services-with-the-new-docker-stack-and-a-compose-file-2/)
  - I have issues with local host, solution: [github issue](https://github.com/ansible/ansible/issues/33132)  


- ansible "msg": "Error starting project UnixHTTPConnectionPool(host='localhost', port=None): Read timed out. (read timeout=60)"}   
  - Same issue, solution [github](https://github.com/ansible/ansible-container/issues/147). Do this on docker host:
    > export DOCKER_CLIENT_TIMEOUT=500   
      export COMPOSE_HTTP_TIMEOUT=500  

  - Also try `export ANSIBLE_CONFIG="/Users/jean/Documents/GitHub/JR_Stacks/stack_for_mac/ansible/ans-menu"`
