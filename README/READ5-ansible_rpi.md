# Setting up Ansible on RPi

---> Back to the README file with the [Table of Contents](../README.md).

https://arnesonium.com/2016/11/installing-ansible-2-2-0-on-a-raspberry-pi/

- Pre-reqs
  `sudo apt install asciidoc devscripts python-dev libffi-dev libssl-dev cdbs sshpass -y`

- cd /tmp
- git clone git://github.com/ansible/ansible.git --recursive
- Check out latest versions:
  > git tag -l
    git checkout v2.2.0.0-1
    make deb

- See web instructions

## Linux User management

### Manage the same users accross servers
- [thornelabs blog](https://thornelabs.net/2014/04/19/ansible-manage-the-same-users-across-servers-with-different-passwords.html)


###---- not working ----
#### Installing on RPi
iotp@host$ git clone git://github.com/ansible/ansible.git --recursive
source ~/ansible/hacking/env-setup
nano ~/.profile
  - source ~/ansible/hacking/env-setup -q   # -q makes it silent

#### Updating ansible
cd ~/ansible
git pull --rebase
git submodule update --init --recursive

#### Host file

mkdir ~/ansibleapps && ~/ansibleapps
nano /etc/ansible/hosts
  > - [testpi]
      dabar3

---> Back to the README file with the [Table of Contents](../README.md).
