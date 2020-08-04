[Install LAMP Stack CentOS 8 rhel 8](https://www.linuxbabe.com/redhat/install-lamp-stack-centos-8-rhel-8)
* `sudo dnf install -y httpd httpd-tools`
* `sudo systemctl start httpd`
* `sudo systemctl enable httpd`
* `sudo systemctl status httpd`
* `httpd -v`
* `sudo firewall-cmd --permanent --zone=public --add-service=http`
* `sudo systemctl reload firewalld`
* `sudo apachectl configtest`
* `sudo vim /etc/httpd/conf.d/servername.conf`
  * Add the following line in this file.
    * ServerName localhost
  * `sudo systemctl reload httpd`
* `sudo apachectl configtest`

* Disable Trace
  * `curl -i -X TRACE 127.0.0.1`
  * `vim /etc/httpd/conf/httpd.conf`
    * Go to the end of the file and type the following
    * \# Disable Trace
    * TraceEnable off
  * `sudo systemctl restart httpd`
  * `curl -i -X TRACE 127.0.0.1`

* `sudo vim /etc/httpd/conf/httpd.conf`
  * \# ServerName www.example.com:80 * Optional since already working
  * \# Deny access to the entirety of your server's filesystem. You must explicitly permit access to web content directories in other <Directory> blocks below.<br />
      <Directory \/><br />
        Options FollowSymLinks<br />
        AllowOverride none<br />
      <\/Directory>
  * DocumentRoot "/var/www/html/"
  * \# Relax access to content within /var/www.<br />
      <Directory "/var/www"><br />
        AllowOverride None<br />
        Require all granted<br />
      <\/Directory>
  * \# Further relax access to the default document root:<br />
      <Directory "/var/www/html"><br />
        Options FollowSymLinks<br />
        AllowOverride None<br />
        Order allow,deny<br />
        Allow from all<br />
      <\/Directory>
  * \# DirectoryIndex: sets the file that Apache will serve if a directory is requested.<br />
      \<IfModule dir_module><br />
        DirectoryIndex index.html index.php<br />
      <\/IfModule>
  * \# The following lines prevent .htaccess and .htpasswd files from being viewed by Web clients.<br />
      <Files ~ "^\\.ht"><br />
        Order allow,deny<br />
        Deny from all<br />
      <\/Files>
  * \# "/var/www/cgi-bin" should be changed to whatever your ScriptAliased CGI directory exists, if you have that configured.<br />
      <Directory "/var/www/cgi-bin"><br />
        AllowOverride None<br />
        Options None<br />
        Order allow,deny<br />
        Allow from all<br />
      <\/Directory>

* `sudo systemctl restart httpd`
* `sudo apachectl configtest`
* `httpd -v`
