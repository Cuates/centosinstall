[freetds-1.1.20](https://centos.pkgs.org/8/epel-x86_64/freetds-1.1.20-1.el8.x86_64.rpm.html)<br />
[Cant Install Freetds Via Yum Package Manager](https://stackoverflow.com/questions/20179649/cant-install-freetds-via-yum-package-manager)
* `sudo dnf install -y epel-release`
* `sudo dnf install -y freetds freetds-devel`
* `sudo vim /etc/freetds.ini`
  * Uncomment the following
    * text size = 64512;
  * Add the following
    * [MSSQL]<br />
      host = SERVERNAME<br />
      port = 1433<br />
      tds version = 8.0
* `tsql -C`
