[How To Install Microsoft SQL Server On RHEL CentOS](https://computingforgeeks.com/how-to-install-microsoft-sql-server-on-rhel-centos/)<br />
[How To Install Microsoft SQL Server 2019 In CentOS 8](https://developpaper.com/how-to-install-sql-server-2019-in-centos8/)<br />
[How To Setup A Firewall With Firewalld On CentOS 7](https://linuxize.com/post/how-to-setup-a-firewall-with-firewalld-on-centos-7/
)<br />
[Polybase Linux Setup](https://docs.microsoft.com/en-us/sql/relational-databases/polybase/polybase-linux-setup?view=sql-server-ver15)<br />
[SQL Server Linux Faq](https://docs.microsoft.com/en-us/sql/linux/sql-server-linux-faq?view=sql-server-2017#general-questions)<br />

* Add the Microsoft SQL Server 2019 repository
  * `sudo curl https://packages.microsoft.com/config/rhel/8/mssql-server-2019.repo -o /etc/yum.repos.d/mssql-server-2019.repo`
  * `sudo curl https://packages.microsoft.com/config/rhel/8/prod.repo -o /etc/yum.repos.d/msprod.repo`

* Install MS SQL server on RHEL 8 / CentOS 8
  * `sudo dnf makecache`
  * `sudo dnf clean all`
  * `sudo dnf -y install mssql-server`
    * **WAIT FOR THIS TO FINISH**

* Install SQL Server command-line tools
  * `sudo dnf -y install mssql-tools unixODBC-devel`
  * `sudo dnf -y update mssql-tools`
  * `sudo systemctl restart mssql-server`

* Accept License
  * YES Enter
  * YES Enter

* Confirm installation
  * `rpm -qi mssql-server`
  * `dnf info mssql-server`
  * `rpm -qi mssql-tools`

* Initialize MS SQL Database Engine
  * `sudo /opt/mssql/bin/mssql-conf setup`

* Select an edition you’d like to use
  * \# Enter
    * **NOTE** DOES NOT ASK FOR LICENSE KEY

* Accept the license terms
  * Yes Enter

* Set SQL Server system administrator password
  * Password Enter
  * Confirm Password Enter

* The service should be started and set to start at boot
  * `systemctl status mssql-server.service`
  * `systemctl is-enabled mssql-server.service`

* Add /opt/mssql/bin/ to your $PATH variable
  * `echo 'export PATH=$PATH:/opt/mssql/bin:/opt/mssql-tools/bin' | sudo tee /etc/profile.d/mssql.sh`

* Source the file to start using MS SQL executable binaries in your current shell session
  * `source /etc/profile.d/mssql.sh`

* If you have an active Firewalld service, allow SQL Server ports for remote hosts to connect
  * `sudo firewall-cmd --get-services`
  * `sudo firewall-cmd --zone=public --permanent --add-service=mssql`
  * `sudo firewall-cmd --reload`
  * `sudo firewall-cmd --list-services`
  * `sudo firewall-cmd --info-service mssql`

* Install Polybase
  * `sudo dnf -y install mssql-server-polybase`
  * `sudo systemctl restart mssql-server`
  * `sudo dnf -y install mssql-server-polybase-hadoop`
  * `sudo systemctl restart mssql-launchpadd`

**USAGE**<br />
* Test SQL Server
  * Connect to the SQL Server and verify it is working
    * `sqlcmd -S localhost -U SA`

* Authenticate with the password set above
  * Password Enter

* Show Database users
  * `select name from sysusers;`

* Create a test database
  * `create database mytestdb`
  * `select name from sys.databases`
  * `go`
  * `use mytestdb`
  * `create table inventory (id int, name nvarchar(50), quantity int)`
  * `insert into inventory values (1, 'banana', 150);`
  * `go`
  * `insert into inventory values (2, 'orange', 154);`
  * `go`
  * `select top 1 * from inventory;`
  * `go`

* Show databases on the SQL Server
  * `select name, database_id from sys.databases;`
  * `go`

* Drop a database
  * `use master;`
  * `go`
  * `drop database mytestdb;`
  * `go`
  * `select name, database_id from sys.databases;`
  * `go`
  * `exit`
