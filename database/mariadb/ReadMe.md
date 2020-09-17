[How To Install MariaDB On CentOS 8](https://www.linode.com/docs/databases/mariadb/how-to-install-mariadb-on-centos-8/)<br />
[MariaDB Install](https://www.server-world.info/en/note?os=CentOS_8&p=mariadb&f=1)<br />
[MySQL Remote Access](https://linuxize.com/post/mysql-remote-access/)<br />
[Allow Remote Access to MariaDB Server](https://www.mynotepaper.com/allow-remote-access-to-mariadb-server-on-rhel-centos)<br />
[Host 'xxx.xx.xxx.xxx' is not allowed to connect to this MySQL server](https://stackoverflow.com/questions/1559955/host-xxx-xx-xxx-xxx-is-not-allowed-to-connect-to-this-mysql-server)<br />
[Beekeeper Studio](https://www.beekeeperstudio.io/)<br />
[Install LAMP Stack CentOS 8 rhel 8](https://www.linuxbabe.com/redhat/install-lamp-stack-centos-8-rhel-8)<br />
[How To Create And Manage Databases In MySQL And MariaDB On A Cloud Server](https://www.digitalocean.com/community/tutorials/how-to-create-and-manage-databases-in-mysql-and-mariadb-on-a-cloud-server)<br />
[Set Value Of Character Set Client To utf8mb4](https://dba.stackexchange.com/questions/59126/set-value-of-character-set-client-to-utf8mb4)<br />
[Change MySQL Default Character Set To utf-8 In my cnf](https://stackoverflow.com/questions/3513773/change-mysql-default-character-set-to-utf-8-in-my-cnf)<br />
[MariaDB](https://mariadb.org/download/)
* `sudo vim /etc/yum.repo.d/MariaDB.repo`
  * \# MariaDB 10.5 [Stable] CentOS repository list - created 2020-07-30 23:39 UTC<br />
    \# [MariaDB Download Test](https://mariadb.org/download-test/)<br />
    **PASTE BELOW INTO FILE**<br />
    [mariadb]<br />
    name = MariaDB<br />
    baseurl = http://sfo1.mirrors.digitalocean.com/mariadb/yum/10.5/centos8-amd64<br />
    module_hotfixes=1<br />
    gpgkey=http://sfo1.mirrors.digitalocean.com/mariadb/yum/RPM-GPG-KEY-MariaDB<br />
    gpgcheck=1<br />
* `sudo dnf clean packages`
* `sudo dnf install -y mariadb-server mariadb mysql-devel`
* `sudo systemctl start mariadb`
* `sudo systemctl enable mariadb`
* `sudo systemctl status mariadb`
* `sudo mysql_secure_installation`
  * Enter current password for root (enter for none): Enter
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
* Log into the router and port forward mysql (port 3306) to the Linux machine, so traffic can be redirected (this is optional)
* `sudo mysql`
  * select user,host,password from mysql.user;
  * show databases;
  * GRANT ALL ON \*.\* TO user_name@ip_address IDENTIFIED BY 'user_password' WITH GRANT OPTION;
    * IP_Address means user can login from a specific IP address
    * "WITH GRANT OPTION" is optional
  * FLUSH PRIVILEGES;
    * The above command is to apply changes 
  * GRANT ALL ON \*.\* TO user_name@ip_address IDENTIFIED BY 'user_password' WITH GRANT OPTION;
    * '%' means user can login from any IP
    * "WITH GRANT OPTION" is optional
  * FLUSH PRIVILEGES;
    * The above command is to apply changes 
  * exit;
* `mariadb --version`

**IMPORTANT NOTE**
* Need to grant permissions within the database to a specific user and IP for external database access

**Setup Database For utf8mb4**
* Modify client.cnf File
  * sudo vim /etc/my.cnf.d/client.cnf
    * WAS
      * [client]<br />
        [client-mariadb]

    * IS
      * [client]<br />
        default-character-set = utf8mb4<br />
        [client-mariadb]
        default-character-set = utf8mb4
    * Save and Exit

  * `sudo vim /etc/my.cnf.d/mysql-client.cnf`
    * WAS
      * [mysql]<br />
        [mysql_upgrade]<br />
        [mysqladmin]<br />
        [mysqlbinlog]<br />
        [mysqlcheck]<br />
        [mysqldump]<br />
        [mysqlimport]<br />
        [mysqlshow]<br />
        [mysqlslap]<br />
    * IS
      * [mysql]<br />
        default-character-set = utf8mb4<br />
        [mysql_upgrade]<br />
        [mysqladmin]<br />
        [mysqlbinlog]<br />
        [mysqlcheck]<br />
        [mysqldump]<br />
        [mysqlimport]<br />
        [mysqlshow]<br />
        [mysqlslap]<br />
    * Save and Exit

* Modify server.cnf File
  * `sudo vim /etc/my.cnf.d/server.cnf`
    * WAS
      * [server]<br />
        [mysqld]<br />
        [galera]<br />
        [embedded]<br />
        [mariadb]<br />
        [mariadb-10.5]<br />

    * IS
      * [server]<br />
        [mysqld]<br />
        character-set-client-handshake = FALSE<br />
        character-set-server = utf8mb4<br />
        collation-server = utf8mb4_unicode_520_ci<br />
        init-connect = 'SET NAMES utf8mb4 COLLATE utf8mb4_unicode_520_ci'<br />
        init-connect = 'SET collation_connection = utf8mb4_unicode_520_ci'<br />
        [galera]<br />
        [embedded]<br />
        [mariadb]<br />
        [mariadb-10.5]<br />
    * Save and Exit

* Restart MariaDB Services
  * `sudo systemctl restart mariadb`

* Repair And Optimize
  * `mysqlcheck -u root -p --auto-repair --optimize --all-databases`

* Check Database Took Hold Of New Modifications
  * `select schema_name, default_character_set_name, default_collation_name from information_schema.schemata where schema_name not in ('mysql', 'information_schema', 'performance_schema', 'sys');`
  * `select * from information_schema.columns where table_name like 'media%';`
  * `show session variables where Variable_name like 'character_set\_%' or Variable_name like 'collation%';`
  * `show global variables where Variable_name like 'character_set\_%' or Variable_name like 'collation%';`
  * `show global variables like 'init_connect';`
  * `show variables like '%_server' ;`
  * `show variables like 'char%';`
  * `show variables like 'collation%';`
  * See which procedures have not been updated to the server’s new character_set_client, collation_connection and Database Collation values
    * `show procedure status;`
