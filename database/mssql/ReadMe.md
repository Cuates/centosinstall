[How To Install Microsoft SQL Server On RHEL CentOS](https://computingforgeeks.com/how-to-install-microsoft-sql-server-on-rhel-centos/)<br />
[How To Install Microsoft SQL Server 2019 In CentOS 8](https://developpaper.com/how-to-install-sql-server-2019-in-centos8/)<br />
[How To Install Microsoft SQL Server 2019 On CentOS 7 Fedora](https://computingforgeeks.com/how-to-install-microsoft-sql-2019-on-centos-7-fedora/)<br />
[How To Setup A Firewall With Firewalld On CentOS 7](https://linuxize.com/post/how-to-setup-a-firewall-with-firewalld-on-centos-7/
)<br />

* `sudo firewall-cmd --permanent --add-service=mssql`
* `sudo firewall-cmd --reload`
* `sudo firewall-cmd --list-services`
* `sudo firewall-cmd --info-service mssql`
