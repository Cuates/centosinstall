[Enable SSH CentOS 8](https://linuxhint.com/enable_ssh_centos8/)<br />
[Install Enable OpenSSH Server CentOS 8 Linux](https://www.how2shout.com/linux/install-enable-openssh-server-centos-8-linux/)<br />
[Install SSH Server On Redhat 8](https://linuxconfig.org/install-ssh-server-on-redhat-8)<br />
[Redhat 8 Open And Close Ports](https://linuxconfig.org/redhat-8-open-and-close-ports)<br />
[Man SSHD Permit Root Login](https://man.openbsd.org/sshd_config#PermitRootLogin)
* `sudo dnf install -y openssh-clients openssh-server`
* `sudo systemctl status sshd`
* `sudo systemctl start sshd`
* `sudo systemctl enable sshd`
* `ifconfig` (Get IP address of the Linux machine)
* Log into the router and port forward SSH (port 22) to the Linux machine, so traffic can be redirected
* `sudo vim /etc/ssh/sshd_config`
  * WAS
    * PermitRootLogin=yes
    * OR
    * #PermitRootLogin prohibit-password
  * IS
    * PermitRootLogin=no
    * OR
    * PermitRootLogin no
  * `sudo systemctl restart sshd`
* `sudo systemctl enable --now cockpit.socket`
  * Activate the web console with the above command (**This is optional and is more for a GUI visual aid**)
  * After ssh login, the terminal shows a message
    * Web console: https://localhost:9090/ or https://IP_ADDRESS:9090/

[Using Selinux](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/8/html-single/using_selinux/index)<br />
[Redhat Install Semanage Selinux Command Rpm](https://www.cyberciti.biz/faq/redhat-install-semanage-selinux-command-rpm/)
* `ssh -V`

* Search for semanage port if there are issues
