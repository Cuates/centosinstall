[How To Install MariaDB On CentOS 8](https://www.linode.com/docs/databases/mariadb/how-to-install-mariadb-on-centos-8/)
[MariaDB Install](https://www.server-world.info/en/note?os=CentOS_8&p=mariadb&f=1)
[MySQL Remote Access](https://linuxize.com/post/mysql-remote-access/)
[Beekeeper Studio](https://www.beekeeperstudio.io/)
[Install LAMP Stack CentOS 8 rhel 8](https://www.linuxbabe.com/redhat/install-lamp-stack-centos-8-rhel-8)
[MariaDB](https://mariadb.org/download/)
* `sudo vim /etc/yum.repo.d/MariaDB.repo`
  * \# MariaDB 10.5 [Stable] CentOS repository list - created 2020-07-30 23:39 UTC<br />
    [MariaDB Download Test](https://mariadb.org/download-test/)<br />
    [mariadb]<br />
    name = MariaDB<br />
    baseurl = http://sfo1.mirrors.digitalocean.com/mariadb/yum/10.5/centos8-amd64<br />
    module_hotfixes=1<br />
    gpgkey=http://sfo1.mirrors.digitalocean.com/mariadb/yum/RPM-GPG-KEY-MariaDB<br />
    gpgcheck=1<br />
* `sudo dnf install -y mariadb-server mariadb`
  * Is this ok: y Enter
  * Is this ok: y Enter
  * Is this ok: y Enter
* `sudo systemctl start mariadb`
* `sudo systemctl enable mariadb`
* `sudo systemctl status mariadb`
* `sudo mysql_secure_installation`
  * Switch to unix_socket authentication: Y Enter
  * Change the root password? Y Enter
    * New password: PASSWORD_HERE
    * Re-enter new password:
  * Remove anonymous users: Y Enter
  * Disallow root login remotely: Y Enter
  * Remove test database and access to it: Y Enter
  * Reload privilege tables now: Y Enter
* `mysql -u root -p`
  * exit;
* `sudo firewall-cmd --permanent --add-service=mysql`
* `sudo firewall-cmd --reload`
* `sudo firewall-cmd --list-services`
* `sudo firewall-cmd --info-service mysql`
* Log into the router and port forward mysql (port 3306) to the Linux machine, so traffic can be redirected
* `sudo mysql`
  * select user,host,password from mysql.user;
  * show databases;
  * GRANT ALL ON *.* TO user_name@'ip_address' IDENTIFIED BY 'user_password';
  * exit;
* `mariadb --version`

**IMPORTANT NOTE**
* Need to grant permissions within the database to a specific user and IP for external database access
