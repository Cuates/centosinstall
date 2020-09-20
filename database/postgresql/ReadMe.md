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
[Placeholder](Placeholder)

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

* User Drop
  * `drop user <username>;`

* Table Grant Privileges
  * `grant all privileges on all tables in schema public to <username>;`

* Sequence Grant Privileges
  * `grant all privileges on all sequences in schema public to <username>;`

* Access Future Objects in the schema Automatically
  * `alter default privileges in schema public grant all on tables to <username>;`

* Access Future Objects in the Database Automatically
  * `alter default privileges grant all on tables to <username>;`

* Sequence Create **NOTE This is for auto_increment**
  * `create sequence <tablename>_<tableID)_seq;`

* Table Create
  * `create table if not exists <tablename>(`<br />
    `tableID bigint not null default nextval('<tablename>_<tableID>_seq'),`<br />
    `columnOne int not null,`<br />
    `columnTwo varchar(255) not null,`<br />
    `columnThree text default null,`<br />
    `columnFour bit(1) not null default b'0',`<br />
    `columnFive timestamp not null default current_timestamp,`<br />
    `columnSix timestamp default current_timestamp,`<br />
    `constraint PK_<tablename>_<columnOne> primary key (columnOne)`<br />
  `);`

* Ownership Create **NOTE This is for auto_increment**
  * `alter sequence <tablename>_<tableID>_seq owned by <tablename>.<tableID>;`
  
* Create Index **NOTE To create an index on the expression lower(<columnname>), allowing efficient case-insensitive searches**
  * `create index IX_<tablename>_columnTwo on <tablename> ((lower(columnTwo)));`

* Sequence Grant Permissions to all
  * `grant usage, select on all sequences in schema public to <username>;`

* Table Columns
  * `\d <tablename>`
  * `select * from information_schema.columns where table_name = '<tablename>';`

* Table Describe
  * `\d+ <tablename>`

* Sequence
  * `select c.relname from pg_class c where c.relkind = 'S';`

* Sequence Last Value
  * `select last_value from <tablename>_<tableID>_seq;`

* Table Drop
  * `drop table if exists <tablename>;`

* Table Select
  * `select tableID, columnOne, columnTwo, columnThree, columnFour, columnFive, columnSix from <tablename>;`

* Table Insert
  * `insert into <tablename> (columnOne, columnTwo, columnThre, columnFour, columnFive, columnSix) values (0, 'columnTwo', 'columnThree', 1, current_timestamp, current_timestamp);`

* Table Update
  * `update <tablename> set columnFour = 1 where columnFour = 0;`

* Table Delete
  * `delete from <tablename> where tableID = 1;`

* Table Truncate
  * `truncate table <tablename>;`

* Table Truncate And Reseed Identity
  * `truncate table <tablename> restart identity;`
