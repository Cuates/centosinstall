[UnixODBC 2.3.7-1](https://centos.pkgs.org/8/centos-appstream-aarch64/unixODBC-2.3.7-1.el8.aarch64.rpm.html)<br />
[Configure Odbc Mysql CentOS](http://www.uptimemadeeasy.com/linux/configure-odbc-mysql-centos/)<br />
[CentOS 8 PHP 72 And MS SQL Server](https://stackoverflow.com/questions/58181436/centos-8-php-7-2-and-ms-sql-server)<br />
[Install Oracle Odbc Driver On CentOS](http://www.uptimemadeeasy.com/linux/install-oracle-odbc-driver-on-centos/)<br />
[How To Connect To SQL Server Using FreeTDS ODBC](https://stackoverflow.com/questions/57350910/how-to-connect-to-sql-server-using-freetds-odbc/)
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
