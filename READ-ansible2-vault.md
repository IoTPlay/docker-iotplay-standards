## 1. Ansible Vault / Secrets

- Sources:
  - ansible Vaults in playbooks [docs.ansible.com](http://docs.ansible.com/ansible/latest/playbooks_vault.html)
  - A short tutorial on how to use Vault in your Ansible workflow [Tristan Fisher](https://gist.github.com/tristanfisher/e5a306144a637dc739e7)
  - Dan's Cheat Sheets 1 documentation [readthedocs](http://cheat.readthedocs.io/en/latest/ansible/secrets.html)
  - How To Use Vault to Protect Sensitive Ansible Data [digital ocean](https://www.digitalocean.com/community/tutorials/how-to-use-vault-to-protect-sensitive-ansible-data-on-ubuntu-16-04)

#### Ansible Vault commands

  | Action                    | Command                                                           |
  | --------------------------|------------------------------------------------------------------ |
  | Create ensrypted files    | ansible-vault create foo.yml
  | Edit  ....                | ansible-vault edit foo.yml
  | Rekey - chng passwd files | ansible-vault rekey foo.yml bar.yml
  | Encrypt ...               | ansible-vault encrypt foo.yml
  | Dycrypt ...               | ansible-vault decrypt foo.yml
  | View ...                  | ansible-vault view foo.yml
  | Run a playbook            | ansible-playbook site.yml --ask-vault-pass (Deprecated)
  | Prompt for a pwd          | ansible-playbook --vault-id @prompt site.yml
  | Prmpt for Dev vault id    | ansible-playbook --vault-id dev@prompt site.yml


#### Using normal, and encrypted passwords

  - Directory structure in hosts directory:

  .
  ├── . . .
  ├── group_vars/
  │   └── database/
  │       ├── vars
  │       └── vault
  └── . . .

  - To check variables use of hosts:
   > `ansible -m debug -a 'var=hostvars[inventory_hostname]' database`


#### Dealing with passwords

- To use them, they need to be hashed to shadow passwords:
  - Rather work with the Vault !!!
  - use    : pip install passlib (does not work on Mac)
  - Command: mkpasswd --method=sha-512
  - python -c 'import crypt; print crypt.crypt("iotp", "$6$random_salt")'
  - Sources:
    - usr & pwd with ansible: [blog Gabriel Birke](https://lebenplusplus.de/2017/04/19/creating-users-and-their-passwords-with-ansible/)

#### Dealing with ssh keys

Good answer on storing keys in ansible-vault [stack overflow](https://stackoverflow.com/questions/29392369/ansible-ssh-private-key-in-source-control)

- `ansible-vault` can operate on any file type. Just encrypt the file with:
  `ansible-vault encrypt /path/to/local/private_key`

- then install the key:
  ```
  - name: Install a private SSH key
    vars:
      source_key: /path/to/local/private_key
      dest_key: /path/to/remote/private_key
    tasks:
    - name: Ensure .ssh directory exists.
      file:
        dest: "{{ dest_key | dirname }}"
        mode: 0700
        owner: user
        state: directory
    - name: Install ssh key
      copy:
        src: "{{ source_key }}"
        dest: "{{ dest_key }}"
        mode: 0600
        owner: user
  ```
