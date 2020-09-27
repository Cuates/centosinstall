[How To Install Microsoft SQL Server On RHEL CentOS](https://computingforgeeks.com/how-to-install-microsoft-sql-server-on-rhel-centos/)<br />
[How To Install Microsoft SQL Server 2019 In CentOS 8](https://developpaper.com/how-to-install-sql-server-2019-in-centos8/)<br />
[How To Install Microsoft SQL Server 2019 On CentOS 7 Fedora](https://computingforgeeks.com/how-to-install-microsoft-sql-2019-on-centos-7-fedora/)<br />
[How To Setup A Firewall With Firewalld On CentOS 7](https://linuxize.com/post/how-to-setup-a-firewall-with-firewalld-on-centos-7/
)<br />

* Add the Microsoft SQL Server 2019 repository
  * `sudo curl https://packages.microsoft.com/config/rhel/8/mssql-server-2019.repo -o /etc/yum.repos.d/mssql-server-2019.repo`
  * `sudo curl https://packages.microsoft.com/config/rhel/8/prod.repo -o /etc/yum.repos.d/msprod.repo`

* Install MS SQL server on RHEL 8 / CentOS 8
  * `sudo dnf -y install mssql-server`

* Accept License Agreement when you see a prompt
  * YES Enter

* Install SQL Server command-line tools
  * `sudo dnf -y install mssql-tools unixODBC-devel`

* Accept License
  * YES Enter
  * YES Enter

* Confirm installation
  * `rpm -qi mssql-server`
  * `rpm -qi mssql-tools`

* Initialize MS SQL Database Engine
  * `sudo /opt/mssql/bin/mssql-conf setup`

* Select an edition you’d like to use
  * \# Enter

* Accept the license terms
  * Yes

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
  * `sudo firewall-cmd --permanent --add-service=mssql`
  * `sudo firewall-cmd --reload`
  * `sudo firewall-cmd --list-services`
  * `sudo firewall-cmd --info-service mssql`

**USAGE**<br />
* Test SQL Server
  * Connect to the SQL Server and verify it is working
    * `sqlcmd -S localhost -U SA`

* Authenticate with the password set above
  * Password Enter

* Show Database users
  * select name from sysusers;

* Create a test database
  * `CREATE DATABASE mytestDB`
  * `SELECT Name from sys.Databases`
  * `GO`
  * `USE mytestDB`
  * `CREATE TABLE Inventory (id INT, name NVARCHAR(50), quantity INT)`
  * `INSERT INTO Inventory VALUES (1, 'banana', 150); INSERT INTO Inventory VALUES (2, 'orange', 154);`
  * `GO`
  * `SELECT * FROM Inventory LIMIT 1;`

* Show databases on the SQL Server
  * `select name,database_id from sys.databases;`

* Drop a database
  * `DROP DATABASE testDB;`
