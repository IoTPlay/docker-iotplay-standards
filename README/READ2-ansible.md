# Ansible Standards

---> Back to the README file with the [Table of Contents](../README.md).

- Source 1: [ansible-file-layouts](https://leucos.github.io/ansible-files-layout)  
- Youtube video [Ben's IT lessons: Ansible - A Beginner's Tutorial, Part 1](https://youtu.be/icR-df2Olm8)  
- Ansible best practices [docs.ansible.com playbooks](http://docs.ansible.com/ansible/latest/playbooks_best_practices.html)  
- Short quickstart guide [jmkhael blog](http://jmkhael.io/ansible-3/)  
- Setting ansible up on RPi [datahovel](https://datahovel.com/2016/03/20/how-to-setup-the-raspberry-pi-using-ansible/)

## 1. Some useful commands (from Ben's videos)

### a. Get ansible installed on the control host and target hosts:

- Generate a key: `ssh-keygen`
- Copy the key to the target host: `ssh-copy-id target-host`,
  - or, if the ports of ssh were already changed:, `ssh-copy-id -p2279 uid@hostname -f`
  - This you do at `sudo nano /etc/ssh/ssh_config`
- Then install the latest version of ansible from git
- Check the ansible version: `ansible --version`


### b. Ad-hoc commands:

- an ad-hoc command:  `ansible -m ping all`
- Check the hostname: `ansible -m shell -a 'hostname' all`
  - the module : `-m` , and in this case, the module is `shell`
- Check diskspace: `ansible -m shell -a 'df -h' all`
- Check the user `ansible -b -K -m user -a 'name=pi' all`
  - Ask the sudo pwd, if sudo cannot run without pwd: `-K`
  - Run the command with remote user, not local: `-b`
- Get entries from name service switch libs:   
`ansible -m shell -a 'getent passwd | grep pi' all`
- Check O/S of hosts: `ansible all -a "cat /etc/issue.net"`

### c. Roles & Playbooks
- What is a **role**? 'a list of commands executed in order on the target host.'
- What is a **playbook**? To determine which role should be applied to which target machine.
- every **role** in a folder **/roles**, must contain a folder **./tasks**, which contains a file `main.yml`
- Run the test playbook:  
`ansible-playbook -K ./playbooks/playbook_nano.yml `


### d. Example Roles:
1. **Copying files**. A demo of a role, this is the main.yml file. The source where to put files to be copied: `../files`
>`- name: "A demo of how to copy files to target"`  
`copy: src=../files/testfile.ini owner=root group=root mode=0644`

2. **Check if a file exist before acting**.
>`- name: "Removing a file if it exist"`   
`  shell: creates=/home/pi/data then the command`

### e. Production Playbooks --
Following the instructions to run the playbooks that are working on home network. Run all these commands from the ansible home directory, `./folder/ansible`. It uses the hosts file in the ansible directory:
- Upgrading debian o/s:

>`ansible-playbook ./playbooks/debian-upgrade.yml`

### f. Useful commands

- List the facts of remote hosts gathered: `ansible all -m setup --tree /tmp/facts`
- About gather_facts [data essential](https://www.data-essential.com/ansible-how-to-collect-information-about-remote-hosts-with-gathers-facts/)

**From [liquidat](https://liquidat.wordpress.com/2016/02/29/useful-options-ansible-cli/) **
- Listing affected hosts: `ansible-playbook --list-hosts playbook.yml`  
- List tasks            : `ansible-playbook --list-tasks playbook.yml`  
- List all tags         : `ansible-playbook --list-tags  playbook.yml`  
- Running in test mode  : `ansible-playbook --check      playbook.yml`  
- Tasks step by step    : `ansible-playbook --step       playbook.yml`  
- Showing diffs         : `ansible-playbook --diff       playbook.yml`  

**From [github andreicristianpetcu: An Ansible Summary:](https://gist.github.com/andreicristianpetcu/b892338de279af9dac067891579cad7d) **  
- Config files  
- Patterns & Hosts files  
- Variables files  
- inventory parameters  
- [Playbooks](https://gist.github.com/andreicristianpetcu/b892338de279af9dac067891579cad7d#playbooks)  
  - plays  
  - [task definitions](https://gist.github.com/andreicristianpetcu/b892338de279af9dac067891579cad7d#task-definitions)  
- Roles  
- [Modules](https://gist.github.com/andreicristianpetcu/b892338de279af9dac067891579cad7d#modules), and on   [docs.ansible.com](http://docs.ansible.com/ansible/latest/modules_by_category.html)  
  - Above has a link to modules by cat on docs.ansible.com  
  - List all modules: `ansible-doc --list`  
  - [Docker modules](http://docs.ansible.com/ansible/latest/list_of_cloud_modules.html#docker)  
  - [MariaDB modules](http://docs.ansible.com/ansible/latest/list_of_database_modules.html)  
- Variables, substitutes, sources, built-in, facts, ...  
- Filters  
- Lookups  
- Conditions  
- Loops  
- Tags  
- [Commands Lines](https://gist.github.com/andreicristianpetcu/b892338de279af9dac067891579cad7d#command-lines) for : 1) ansible, 2) ansible-playbook, 3) ansible-vault, 4) ansible-doc, 5) ansible-galaxy, 6) ansible-pull  


From [docs.ansible.com playbooks tips and tricks](http://docs.ansible.com/ansible/latest/playbooks_intro.html#tips-and-tricks)
- To check the syntax of a playbook, use `ansible-playbook with the --syntax-check`

From [ansible Rough Guide](http://zenpackers.readthedocs.io/en/latest/ansible.html)


### g. Ansible Module list
[module list](http://docs.ansible.com/ansible/latest/modules_by_category.html)

### h. Installing ansible

- Installing: `sudo pip install ansible`
- Upgrading: `sudo pip install ansible --upgrade`

---------------

## 2. Ansible-Galaxy

### Installing from ansible-galaxy

- Galaxy landing page [galaxy.ansible.com](https://galaxy.ansible.com)
  - Install a role: `$ ansible-galaxy install username.rolename`

- to install in your chosen directory: `ansible-galaxy with the -p ROLES_PATH or --roles-path=ROLES_PATH`
- the command:  
`ansible-galaxy [delete|import|info|init|install|list|login|remove|search|setup] [--help] [options] ...`

- installing:
  - `ansible-galaxy login`, and enter your github uid / pwd.
  - Then you can install: `ansible-galaxy import github_user github_repo`

- Deleting:
    - `ansible-galaxy delete github_user github_repo`

- Put the Roles centrally, like ~/.ansible
    modify each project's ansible.cfg to tell ansible to look for roles in that master folder in addition to the local project folder.

    Sample ansible.cfg:

    [defaults]
    roles_path = ~/Code/ansible_roles
    Ansible first searches the local project for a role, then searches the roles_path. You can specify multiple paths by separating them with colons.


## 3. Ansible - managing directories on the host

### a. Directories
- Creating a directory, with owner & gp, and if 1+ directories, recurse mode.

  ```
    - name: Creates directory   
      file:  
        path: /src/www  
        state: directory  
        owner: www-data   
        group: www-data   
        mode: 0775  
        recurse: yes   
  ```

### b. Ansible variables

- Intro to ansible variables: [liquidat blog](https://liquidat.wordpress.com/2016/01/26/howto-introduction-to-ansible-variables/)
- [nested variables blog](http://blog.v-studios.com/2014/08/nested-variable-inheritance-with.html)
- Variables received from the ansible command line.
```
ansible-playbook release.yml --extra-vars "version=1.23.45 other_variable=foo"
```

---
## General Ansible HowTo & Tips. Dealing with Errors

This general howto and tips to be moved to a central folder, move it around as we work.

### a. Insanely Complete playbooks

- Commented playbook [github phred](https://gist.github.com/phred/2897937)

### b. General tips and tricks

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


#### Only running subset of tasks in a Playbook

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

---> Back to the README file with the [Table of Contents](../README.md).
