## Setting up Ansible on RPi

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
