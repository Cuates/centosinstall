[PostgreSQL Download](https://www.postgresql.org/download/linux/redhat/)
* `sudo dnf module list postgresql`
* `sudo dnf module -y enable postgresql:12`
* `sudo dnf install -y postgresql-server postgresql postgresql-devel  postgresql-odbc`
* `sudo postgresql-setup --initdb`
* `sudo systemctl start postgresql`
* `sudo systemctl enable postgresql`
* `sudo systemctl status postgresql`
* `sudo -i -u postgres`
  * `psql`
  * `\q`
  * `exit`
* `postgres --version`

[Install PostgresSQL And pgAdmin In CentOS 8](https://www.tecmint.com/install-postgressql-and-pgadmin-in-centos-8/)<br />
[How To Install Postgres On Redhat 8](https://linuxconfig.org/how-to-install-postgres-on-redhat-8)<br />
[How To Install PostgreSQL On rhel 8](https://www.itzgeek.com/how-tos/linux/centos-how-tos/how-to-install-postgresql-on-rhel-8.html)
* `psql`
  * `\password postgres`
  * PASSWORD_HERE
  * `exit`
* `sudo vim /var/lib/pgsql/data/postgresql.conf`
  * WAS
    * listen_addresses = 'localhost'
  * IS
    * listen_addresses = '*'
  * Save and Quit
* `sudo systemctl restart postgresql`
* `sudo netstat -antup | grep 5432`
* `sudo vim /var/lib/pgsql/data/pg_hba.conf`
  * WAS
    * host    all             all             127.0.0.1/32            ident
    * host    all             all             ::1/128                 ident
  * IS
    * host    all             all             127.0.0.1/32            md5
    * host    all             all             0.0.0.0/0               md5
    * host    all             all             ::1/128                 md5
  * Save and Quit
* `sudo systemctl restart postgresql`
* `sudo firewall-cmd --zone=public --permanent --add-service=postgresql`
* `sudo firewall-cmd --reload`
