[Install LAMP Stack CentOS 8 rhel 8](https://www.linuxbabe.com/redhat/install-lamp-stack-centos-8-rhel-8)
* `sudo dnf install -y httpd httpd-tools`
* `sudo systemctl start httpd`
* `sudo systemctl enable httpd`
* `sudo systemctl status httpd`
* `httpd -v`
* `sudo firewall-cmd --permanent --zone=public --add-service=http`
* `sudo systemctl reload firewalld`
* `sudo apachectl configtest`
* Create a new configuration file named servername.conf under /etc/httpd/conf.d/ directory
  *`sudo vim /etc/httpd/conf.d/servername.conf`
    * Add the following line in this file.
      * <pre>
        ServerName localhost
        </pre>
  * `sudo systemctl reload httpd`
* `sudo apachectl configtest`

* Disable Trace
  * `curl -i -X TRACE 127.0.0.1`
  * `vim /etc/httpd/conf/httpd.conf`
    * <pre>
      Go to the end of the file and type the following
      # Disable Trace
      TraceEnable off
      </pre>
  * `sudo systemctl restart httpd`
  * `curl -i -X TRACE 127.0.0.1`

* `sudo vim /etc/httpd/conf/httpd.conf`
  * <pre>
    # ServerName www.example.com:80 * Optional since already working
    # Deny access to the entirety of your server's filesystem. You must explicitly permit access to web content directories in other &lt;Directory&gt; blocks below.
    &lt;Directory \/&gt;
      Options FollowSymLinks
      AllowOverride none
    &lt;\/Directory&gt;
    DocumentRoot "/var/www/"

    # Relax access to content within /var/www.
      &lt;Directory "/var/www"&gt;
        AllowOverride None
        Require all granted
      &lt;\/Directory&gt;

    # Further relax access to the default document root:
      &lt;Directory "/var/www/html"&gt;
        Options FollowSymLinks
        AllowOverride None
        Order allow,deny
        Allow from all
      &lt;\/Directory&gt;

    # DirectoryIndex: sets the file that Apache will serve if a directory is requested.
      &lt;IfModule dir_module&gt;
        DirectoryIndex index.html index.php
      &lt;\/IfModule&gt;

    # The following lines prevent .htaccess and .htpasswd files from being viewed by Web clients.
      &lt;Files ~ "^\\.ht"&gt;
        Order allow,deny
        Deny from all
      &lt;\/Files&gt;

    # "/var/www/cgi-bin" should be changed to whatever your ScriptAliased CGI directory exists, if you have that configured.
      &lt;Directory "/var/www/cgi-bin"&gt;
        AllowOverride None
        Options None
        Order allow,deny
        Allow from all
      &lt;\/Directory&gt;
    </pre>

* `sudo systemctl restart httpd`
* `sudo apachectl configtest`
* `httpd -v`
