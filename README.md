# General ReadMe instructions for iotplay Infrastructure, Docker images and other learnings

These instructions are to drive the IoTPlay standardisation for the RaspberryPi and Mac docker images we use. We use Ansible open source edition as agent-less DevOps tool to build the RPi's, the docker images, containers, and all the processes to run the targeted IoTPlay solutions. We also use the Docker Community Edition.

See figure 1 below for the flow we implemented for a client using the tools below.

Links to several README files thart describes the tools we use, and summaries of our learnings, with links on using the tools to build the solutions:

|#| README file                                           | Link
|-|------------------------------------------------------ |------
|0| A Menu system for ansible playbooks                   |[link](https://github.com/IoTPlay/menu_ansible/blob/master/README.md)
|1| Docker Images used in IoTPlay                         |[link](README/READ1-iotplay-dockerimages.md)
|2| Ansible - General                                     |[link](README/READ2-ansible.md)
|3| Ansible Vault: how to deal with secrets               |[link](README/READ3-ansible-vault.md)
|4| Ansible Docker: managing docker                       |[link](README/READ4-ansible_docker.md)
|5| Ansible on Raspberry Pi                               |[link](README/READ5-ansible_rpi.md)
|6| Running IoTPlay on Raspberry Pi - instructions        |[link](README/READ6-RPi.md)
|7| Docker - shortcuts, command, howto's                  |[link](README/READ7-RPi.md)
|8| MariaDB                                               |[link](README/READ8-mariadb.md)
|9| git, howto's                                          |[link](README/READ9-git.md)
|10| Using Node-RED Projects feature for team development |[link](README/READ10-nodered_Projects.md)


Figure 1: DevOps flow.

![](images/DevOps-iotplay-dabar.jpg)
