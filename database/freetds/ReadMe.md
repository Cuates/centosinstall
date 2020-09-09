[freetds-1.1.20](https://centos.pkgs.org/8/epel-x86_64/freetds-1.1.20-1.el8.x86_64.rpm.html)<br />
[Cant Install Freetds Via Yum Package Manager](https://stackoverflow.com/questions/20179649/cant-install-freetds-via-yum-package-manager)<br />
[How To Connect To SQL Server Using FreeTDS ODBC](https://stackoverflow.com/questions/57350910/how-to-connect-to-sql-server-using-freetds-odbc/)
* `sudo dnf install -y epel-release`
* `sudo dnf install -y freetds freetds-devel`
* `sudo vim /etc/freetds.conf` **NOTE was /etc/freetds.ini**
  * Uncomment the following
    * text size = 64512
  * Add the following
    * [MSSQL_FreeTDS_Name]<br />
      host = SERVERNAME<br />
      port = 1433<br />
      tds version = 8.0
* `tsql -C`
* `tsql -S <FreeTDS_Name> -U <username> -P <password>`
