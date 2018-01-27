## Raspberry Pi Stuff

#### Best Practices for Security

- 5 best basic tips:  [blog kamilslab](http://kamilslab.com/2017/01/29/5-best-basic-security-tips-and-tricks-every-raspberry-pi-user-needs-to-take/)
  - create new user
  - delete pi user `sudo userdel -r pi`
  - Install Fail2Ban to ban brute-force attempts
  - Perform Security Updates automatically `sudo apt-get install unattended-upgrades`
  - Setup SSH Key Pairing

- Edit the sshd config file to deny certain users and allow others
  > `sudo nano /etc/ssh/sshd_config`  

  - There are many options but the bare minimum here would be

    >AllowTcpForwarding yes CHANE TO AllowTcpForwarding no
     X11Forwarding yes CHANGE TO X11Forwarding no
     PermitRootLogin no
     DenyUsers  pi
     AllowUsers username

- Dealing with `sudo`:
  - The sudoers file
    > The pi user is included in the `sudoers` file of approved users. To allow other users to act as a superuser you can add the user to the sudo group with usermod, edit the `/etc/sudoers` file, or add them using `sudo visudo`.

  - Rather add a file in `/etc/sudoers.d/` as upgrades will not effect it.  

  - Format of giving access in sudoers: [stack exchange](https://unix.stackexchange.com/questions/18877/what-is-the-proper-sudoers-syntax-to-add-a-user)

- Pi user management:  [raspberrypi.org](https://www.raspberrypi.org/documentation/linux/usage/users.md)

#### Other Things

- bash reference cards [blog tldp](http://www.tldp.org/LDP/abs/html/refcards.html)
