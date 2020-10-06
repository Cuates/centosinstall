[PostgreSQL Download](https://www.postgresql.org/download/linux/redhat/)
* `sudo dnf module list postgresql`
* `sudo dnf module -y enable postgresql:12`
* `sudo dnf install -y postgresql-server postgresql-contrib postgresql postgresql-devel  postgresql-odbc`
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
[How To Install PostgreSQL On rhel 8](https://www.itzgeek.com/how-tos/linux/centos-how-tos/how-to-install-postgresql-on-rhel-8.html)<br />
[Install PostgreSQL 12 CentOS 8](https://sysadminjournal.com/install-postgresql-12-centos-8/)
* `sudo -i -u postgres`
  * `psql`
    * `\password postgres`
    * PASSWORD_HERE
  * `exit`
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

* Alternative Installation for the latest PostgreSQL 13 **Note Cannot install this and a newer/older version at the same time**
[Install PostgresSQL 13 On CentOS  RHEL](https://computingforgeeks.com/install-postgresql-13-on-centos-rhel/)<br />
* Install PostgreSQL 13 on CentOS 8
  * `sudo dnf -qy module disable postgresql`

* Enable PostgreSQL 13 repository
  * `sudo dnf -y install dnf-utils`
  * `sudo yum-config-manager --enable pgdg13`

* Confirm the list of enabled repositories
  * `dnf repolist`

* Check to see if PostgreSQL 13 packages are available on the repository
  * `sudo dnf search postgresql13`

* Install PostgreSQL 13 packages on your CentOS 8
  * `sudo dnf install -y postgresql13-server postgresql13-contrib postgresql13-devel postgresql13`

* Initialize and start database service
  * `sudo /usr/pgsql-13/bin/postgresql-13-setup initdb`

* The database main configuration file is  /var/lib/pgsql/13/data/postgresql.conf
  * `ls /var/lib/pgsql/13/data/`

* Start the PostgreSQL database server and set it to start at boot.
  * `sudo systemctl enable --now postgresql-13`

* Check the service status to confirm it is running.
  * `systemctl status postgresql-13`

* Set PostgreSQL admin user’s password
* `sudo -i -u postgres`
  * `psql`
    * `\password postgres`
    * PASSWORD_HERE
  * `exit`
* `exit`

* `sudo -i -u postgres`
  * `psql`
    * `\password postgres`
    * PASSWORD_HERE
  * `exit`
* `exit`
* `sudo vim /var/lib/pgsql/13/data/postgresql.conf`
  * WAS
    * listen_addresses = 'localhost'
  * IS
    * listen_addresses = '*'
  * Save and Quit
* `sudo systemctl restart postgresql-13`
* `sudo netstat -antup | grep 5432`
* `sudo vim /var/lib/pgsql/13/data/pg_hba.conf`
  * WAS
    * host    all             all             127.0.0.1/32            ident
    * host    all             all             ::1/128                 ident
  * IS
    * host    all             all             127.0.0.1/32            md5
    * host    all             all             0.0.0.0/0               md5
    * host    all             all             ::1/128                 md5
  * Save and Quit **NOTE make sure to tab each column to match the existing column**
* `sudo systemctl restart postgresql-13`

* `sudo firewall-cmd --get-services`
* `sudo firewall-cmd --zone=public --permanent --add-service=postgresql`
* `sudo firewall-cmd --reload`

**USAGE**<br />
[PostgreSQL Grant](https://www.educba.com/postgresql-grant/)<br />
[Create User](https://www.ntchosting.com/encyclopedia/databases/postgresql/create-user/)<br />
[PostgreSQL Create Database](https://www.tutorialspoint.com/postgresql/postgresql_create_database.htm)<br />
[SQL Create Database](https://www.postgresql.org/docs/9.0/sql-createdatabase.html)<br />
[SQL Create Table](https://www.postgresql.org/docs/9.1/sql-createtable.html)<br />
[PostgreSQL Create Table](https://www.tutorialspoint.com/postgresql/postgresql_create_table.htm)<br />
[PostgreSQL Show Databases](https://www.postgresqltutorial.com/postgresql-show-databases/)<br />
[Simulate Create Database If Not Exists For PostgreSQL](https://stackoverflow.com/questions/18389124/simulate-create-database-if-not-exists-for-postgresql)<br />
[SQL Drop Database](https://www.postgresql.org/docs/8.2/sql-dropdatabase.html)<br />
[PostgreSQL Drop Database](https://www.postgresqltutorial.com/postgresql-drop-database/)<br />
[PostgreSQL Select Database](https://www.tutorialspoint.com/postgresql/postgresql_select_database.htm)<br />
[PostgreSQL Show Tables](https://www.postgresqltutorial.com/postgresql-show-tables/)<br />
[PostgreSQL Describe Table](https://www.postgresqltutorial.com/postgresql-describe-table/)<br />
[How To Display All Tables In PostgreSQL](https://kb.objectrocket.com/postgresql/how-to-display-all-tables-in-postgresql-847)<br />
[PostgreSQL Create Table If Not Exists](https://www.dbrnd.com/2018/03/postgresql-create-table-if-not-exists/)<br />
[PostgreSQL Data Types](https://www.postgresqltutorial.com/postgresql-data-types/)<br />
[PostgreSQL Serial](https://www.postgresqltutorial.com/postgresql-tutorial/postgresql-serial/)<br />
[PostgreSQL Integer](https://www.postgresqltutorial.com/postgresql-integer/)<br />
[PostgreSQL Timestamp](https://www.postgresqltutorial.com/postgresql-timestamp/)<br />
[PostgreSQL Primary Key](https://www.postgresqltutorial.com/postgresql-primary-key/)<br />
[Primary Key Constraint](https://www.w3resource.com/PostgreSQL/primary-key-constraint.php)<br />
[Datatype Bit](https://www.postgresql.org/docs/8.2/datatype-bit.html)<br />
[Postgresql Insert](https://www.postgresqltutorial.com/postgresql-insert/)<br />
[List All Sequences In A Postgres db 81 With SQL](https://stackoverflow.com/questions/1493262/list-all-sequences-in-a-postgres-db-8-1-with-sql)<br />
[PostgreSQL Auto Increment](https://www.educba.com/postgresql-auto-increment/)<br />
[View PG Sequences](https://www.postgresql.org/docs/10/view-pg-sequences.html)<br />
[Indexes In PostgreSQL](https://www.educba.com/indexes-in-postgresql/)<br />
[SQL Create Index](https://www.postgresql.org/docs/9.1/sql-createindex.html)<br />
[PostgreSQL Create Index](https://www.postgresqltutorial.com/postgresql-indexes/postgresql-create-index/)<br />
[Postgresql List Indexes](https://www.postgresqltutorial.com/postgresql-indexes/postgresql-list-indexes/)<br />
[Postgresql Truncate Table](https://www.postgresqltutorial.com/postgresql-truncate-table/)<br />
[SQL Truncate](https://www.postgresql.org/docs/9.1/sql-truncate.html)<br />
[Howto Add PostgreSQL User Account](https://www.cyberciti.biz/faq/howto-add-postgresql-user-account/)<br />
[Postgres User Permissions](https://flaviocopes.com/postgres-user-permissions/)<br />
[Postgresql Grant](https://www.educba.com/postgresql-grant/)<br />
[Create User](https://www.ntchosting.com/encyclopedia/databases/postgresql/create-user/)<br />
[SQL Drop Role](https://www.postgresql.org/docs/9.1/sql-droprole.html)<br />
[Cannot Drop PostgreSQL Role Error Cannot Be Dropped Because Some Objects Depe](https://stackoverflow.com/questions/51256454/cannot-drop-postgresql-role-error-cannot-be-dropped-because-some-objects-depe)<br />
[Grant Revoke](https://www.techonthenet.com/postgresql/grant_revoke.php)<br />
[How To Change Owner Of PostgreSQL Database](https://stackoverflow.com/questions/4313323/how-to-change-owner-of-postgresql-database)<br />
[PostgreSQL Drop User](https://www.tutorialkart.com/postgresql/postgresql-drop-user/)<br />
[PostgreSQL List Users](https://www.postgresqltutorial.com/postgresql-list-users/)<br />
[Creating User Database And Adding Access On PostgreSQL](https://medium.com/coding-blocks/creating-user-database-and-adding-access-on-postgresql-8bfcd2f4a91e)<br />
[Permission Denied In Postgres](https://dba.stackexchange.com/questions/36870/permission-denied-in-postgres)<br />
[Error Permission Denied For Sequence Cities Id Seq Using Postgres](https://stackoverflow.com/questions/9325017/error-permission-denied-for-sequence-cities-id-seq-using-postgres)<br />
[List User Defined Functions](https://dataedo.com/kb/query/postgresql/list-user-defined-functions)<br />
[PostgreSQL What Does Grant All Privileges On Database Do](https://serverfault.com/questions/198002/postgresql-what-does-grant-all-privileges-on-database-do)<br />
[SQL Alter Database](https://www.postgresql.org/docs/9.1/sql-alterdatabase.html)<br />
[PostgreSQL Case Insensitive Citext](https://www.logisticinfotech.com/blog/postgresql-case-insensitive-citext/)<br />
[SQL Create Extension](https://www.postgresql.org/docs/12/sql-createextension.html)<br />

* Databases
  * `sudo -i -u postgres`
  * `psql`
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

* Database Alter Owner To Role
  * `alter database <databasename> owner to <username>;`

* Table Alter Owner To Role
  * `alter table <tablename> owner to <username>`

* Procedure Alter Owner To Role
  * `alter procedure <procedurename> owner to <username>`

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

* Drop Extension
  * `drop extension if exists <extension_name>;`

* Create Extension 
  * `create extension if not exists <extension_name> with schema public;`

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

* Table Owner
  * `select`<br />
    `t.table_name,`<br />
    `t.table_type,`<br />
    `c.relname,`<br />
    `c.relowner,`<br />
    `u.usename`<br />
    `from information_schema.tables t`<br />
    `join pg_catalog.pg_class c on t.table_name = c.relname`<br />
    `join pg_catalog.pg_user u on c.relowner = u.usesysid`<br />
    `where`<br />
    `t.table_schema = 'public';`

* Functions and Procedures **NOTE Stored Procedures are new; Before it was Functions only**
  * User Defined Functions Universal
    * `select`<br />
      `n.nspname as function_schema,`<br />
      `p.proname as function_name,`<br />
      `l.lanname as function_language,`<br />
      `case`<br />
        `when l.lanname = 'internal'`<br />
          `then`<br />
            `p.prosrc`<br />
        `else`<br />
          `pg_get_functiondef(p.oid)`<br />
      `end as definition,`<br />
      `pg_get_function_arguments(p.oid) as function_arguments,`<br />
      `t.typname as return_type`<br />
      `from pg_proc p`<br />
      `left join pg_namespace n on p.pronamespace = n.oid`<br />
      `left join pg_language l on p.prolang = l.oid`<br />
      `left join pg_type t on t.oid = p.prorettype`<br />
      `where`<br />
      `n.nspname not in ('pg_catalog', 'information_schema')`<br />
      `order by function_schema, function_name;`<br />
  * User Defined Functions 11+
    * `select`<br />
      `n.nspname as schema_name,`<br />
      `p.proname as specific_name,`<br />
      `case p.prokind`<br />
        `when 'f'`<br />
          `then`<br />
            `'FUNCTION'`<br />
        `when 'p'`<br />
          `then`<br />
            `'PROCEDURE'`<br />
        `when 'a'`<br />
          `then`<br />
            `'AGGREGATE'`<br />
        `when 'w'`<br />
          `then`<br />
            `'WINDOW'`<br />
      `end as kind,`<br />
      `l.lanname as language,`<br />
      `case`<br />
        `when l.lanname = 'internal'`<br />
          `then`<br />
            `p.prosrc`<br />
        `else`<br />
          `pg_get_functiondef(p.oid)`<br />
      `end as definition,`<br />
      `pg_get_function_arguments(p.oid) as arguments,`<br />
      `t.typname as return_type`<br />
      `from pg_proc p`<br />
      `left join pg_namespace n on p.pronamespace = n.oid`<br />
      `left join pg_language l on p.prolang = l.oid`<br />
      `left join pg_type t on t.oid = p.prorettype`<br />
      `where`<br />
      `n.nspname not in ('pg_catalog', 'information_schema')`<br />
      `order by schema_name, specific_name;`
