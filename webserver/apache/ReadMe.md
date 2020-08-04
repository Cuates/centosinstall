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
  * sudo systemctl reload httpd`
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
  * \# ServerName www.example.com:80 * Optional since already working<br />
  * \# Deny access to the entirety of your server's filesystem. You must explicitly permit access to web content directories in other <Directory> blocks below.
      <Directory />
        Options FollowSymLinks
        AllowOverride none
      </Directory>
  * DocumentRoot "/var/www/html/"
  * \# Relax access to content within /var/www.
      <Directory "/var/www">
        AllowOverride None
        Require all granted
      </Directory>
  * \# Further relax access to the default document root:
      <Directory "/var/www/html">
        Options FollowSymLinks
        AllowOverride None
        Order allow,deny
        Allow from all
      </Directory>
  * \# DirectoryIndex: sets the file that Apache will serve if a directory is requested.
      <IfModule dir_module>
        DirectoryIndex index.html index.php
      </IfModule>
  * \# The following lines prevent .htaccess and .htpasswd files from being viewed by Web clients.
      <Files ~ "^\.ht">
        Order allow,deny
        Deny from all
      </Files>
  * \# "/var/www/cgi-bin" should be changed to whatever your ScriptAliased CGI directory exists, if you have that configured.
      <Directory "/var/www/cgi-bin">
        AllowOverride None
        Options None
        Order allow,deny
        Allow from all
      </Directory>

* `sudo systemctl restart httpd`
* `sudo apachectl configtest`
* `httpd -v`
