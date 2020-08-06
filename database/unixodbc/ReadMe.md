[UnixODBC 2.3.7-1](https://centos.pkgs.org/8/centos-appstream-aarch64/unixODBC-2.3.7-1.el8.aarch64.rpm.html)<br />
[Configure Odbc Mysql CentOS](http://www.uptimemadeeasy.com/linux/configure-odbc-mysql-centos/)<br />
[CentOS 8 PHP 72 And MS SQL Server](https://stackoverflow.com/questions/58181436/centos-8-php-7-2-and-ms-sql-server)<br />
[Install Oracle Odbc Driver On CentOS](http://www.uptimemadeeasy.com/linux/install-oracle-odbc-driver-on-centos/)<br />
[How To Connect To SQL Server Using FreeTDS ODBC](https://stackoverflow.com/questions/57350910/how-to-connect-to-sql-server-using-freetds-odbc/)
* `sudo dnf install -y unixODBC unixODBC-devel`
* `sudo vim /etc/odbcinst.ini`
  * Add to file
    * \# ODBC Trace<br />
      [ODBC]<br />
      Trace           = no<br />
      \# Trace           = yes # Change this to yes if you want logs<br />
      TraceFile       = /tmp/unixodbc.log<br />
* `sudo vim /etc/odbc.ini`
  * Add to file
    * [MSSQL]<br />
      Driver          = FreeTDS<br />
      Description     = MS SQL Server 2019<br />
      Trace           = no<br />
      Servername      = FreeTDS_Name<br />
      Port            = 1433<br />
      Database        = DATABASENAME<br />
      UID             = USERNAME<br />
      PWD             = PASSWORD<br />
      TDS_Version     = 8.0
* `isql --version`
