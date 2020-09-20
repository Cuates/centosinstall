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
* `sudo -i -u postgres`
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
  * Save and Quit **NOTE make sure to tab each column to match the existing column**
* `sudo systemctl restart postgresql`
* `sudo firewall-cmd --zone=public --permanent --add-service=postgresql`
* `sudo firewall-cmd --reload`

**USAGE**<br />
[TestONE](TestOne)

* Databases
  * `\l`
  * Select database names from pg database
    * `select datname from pg_database;`
  * Select all records from pg database
    * `select * from pg_database;`
  
* Database Create
  * `create database <databasename>;` **NOTE Does not have 'if exists' when creating databases**

* Database Drop
  * `drop database if exists <databasename>;`

* Database Connect
  * `\c <databasename>;`

* Tables
  * `\dt`

* Roles
  * `\du`

* User Create
  * `create user <username> with password '<password>';`

* Database Grant Privileges
  * `grant all privileges on database <databasename> to <username>;`

* Owner Reassign
  * `reassign owned by <username> to postgres;`

* Owner Drop
  * `drop owned by <username>;`
