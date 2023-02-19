[unixODBC-2.3.7-1.el8.aarch64.rpm](https://centos.pkgs.org/8/centos-appstream-aarch64/unixODBC-2.3.7-1.el8.aarch64.rpm.html)<br />
[Configure ODBC for MySQL on CentOS](https://www.uptimemadeeasy.com/linux/configure-odbc-mysql-centos/)<br />
[Centos 8, PHP 7.2 and MS Sql Server](https://stackoverflow.com/questions/58181436/centos-8-php-7-2-and-ms-sql-server)<br />
[Install and Test Oracle ODBC Drivers on CentOS](http://www.uptimemadeeasy.com/linux/install-oracle-odbc-driver-on-centos/)<br />
[How to connect to SQL Server using FreeTDS ODBC](https://stackoverflow.com/questions/57350910/how-to-connect-to-sql-server-using-freetds-odbc/)<br />

* `sudo dnf install -y unixODBC`
  * unixODBC-devel is not needed anymore
* `sudo vim /etc/odbcinst.ini`
  * Add to file
    * <pre>
      # ODBC Trace
      [ODBC]
      Trace           = no
      # Trace         = yes # Change this to yes if you want logs
      TraceFile       = /tmp/unixodbc.log
      </pre>
* `sudo vim /etc/odbc.ini`
  * Add to file
    * <pre>
      [MSSQL]
      Driver          = FreeTDS
      Description     = MS SQL Server 2019
      Trace           = no
      Servername      = FreeTDS_Name
      Port            = 1433
      Database        = DATABASENAME
      UID             = USERNAME
      PWD             = PASSWORD
      TDS_Version     = 8.0
      </pre>
* `isql --version`
* `isql -v <FreeTDS_Name> <username> <password>`
