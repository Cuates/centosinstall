[Install LAMP Stack CentOS 8 Rhel 8](https://www.linuxbabe.com/redhat/install-lamp-stack-centos-8-rhel-8)<br />
[How To Install PHP On CentOS 8](https://linuxize.com/post/how-to-install-php-on-centos-8/)<br />
[How To Install PHP 73 On Rhel 8](https://www.itzgeek.com/how-tos/linux/centos-how-tos/how-to-install-php-7-3-on-rhel-8.html)<br />
[Linux Installation](https://www.scriptcase.net/docs/en_us/v9/manual/02-scriptcase-installation/06-linux_php/)<br />
[PHP Security Best Practices Tutorial](https://www.cyberciti.biz/tips/php-security-best-practices-tutorial.html)<br />
[Modsecurity With Nginx On CentOS 8](https://www.aventistech.com/kb/modsecurity-with-nginx-on-centos-8/)<br />
[How To Install PHP 8 On CentOS Linux](https://computingforgeeks.com/how-to-install-php-8-on-centos-linux/)<br />
[PHP installation error it is not possible to switch enabled streams of a modul](https://stackoverflow.com/questions/63080021/php-installation-error-it-is-not-possible-to-switch-enabled-streams-of-a-modul)

* If upgrading to a new version of PHP, then perform the upgrading portion below before proceeding with the following commnad.
  * `sudo dnf module -y enable php:remi-7.4`
    * NOTE: The version number above will be the version number you have install on your machine
  * `sudo dnf install -y php php-cli php-common php-curl php-fpm php-mysql php-mysqlnd php-opcache php-gd php-xml php-mbstring php-pdo php-pdo-dblib php-pgsql php-pecl-rar php-odbc php-memcached php-pecl-memcache php-bcmath php-dba php-devel php-embedded php-imap php-intl php-ldap php-mcrypt php-pear php-recode php-pspell php-tidy php-xmlrpc`
  * `sudo systemctl start php-fpm`
  * `sudo systemctl enable php-fpm`
  * `sudo systemctl status php-fpm`
  * `sudo systemctl restart httpd`
  * OR `sudo systemctl restart nginx`
  * `sudo setsebool -P httpd_execmem 1`
  * Test with /var/www/html/info.php
    * \<?php phpinfo(); ?\>
    * Visit website localhost/info.php
    * `sudo rm /var/www/html/info.php` (for security reasons)
  * `sudo vim /etc/php.ini`
    * <pre>
      serialize_precision = -1
      max_execution_time = 240
      date.timezone = America/Los_Angeles
      </pre>
    * Save and Exit
  * `sudo systemctl restart httpd`
  * OR `sudo systemctl restart nginx`
  * `sudo apachectl configtest`
  * OR `sudo nginx -t`
  * `php -r "echo extension_loaded('zip') ? \"Installed\r\n\" : \"Not installed\r\n\";"`
  * `php -v`

  * Configure PHP-FPM
    * Open and modify user and group values
      * `sudo vim /etc/php-fpm.d/www.conf`
        * Apache
          * user = apache
          * group = apache
        * Nginx
          * user = nginx
          * group = nginx
    * Save and Exit
    * Restart php-fpm service
      * `sudo systemctl restart php-fpm`

* If upgrading from 7.4 to 8.1, then
  * Reset the PHP for the new PHP
    * `sudo dnf module reset php`
  * Update the system with any new updates
    *  `sudo dnf update`
  * Remove
    * `sudo dnf remove -y php php-cli php-common php-curl php-fpm php-mysql php-mysqlnd php-opcache php-gd php-xml php-mbstring php-pdo php-pdo-dblib php-pgsql php-pecl-rar php-odbc php-memcached php-pecl-memcache php-bcmath php-dba php-devel php-embedded php-imap php-intl php-ldap php-mcrypt php-pear php-recode php-pspell php-tidy php-xmlrpc`
  * Enable PHP 8.1
    * `sudo dnf module -y enable php:remi-8.1`
  * Install
    * `sudo dnf install -y php php-cli php-common php-curl php-fpm php-mysqlnd php-opcache php-gd php-xml php-mbstring php-pdo php-pdo-dblib php-pgsql php-odbc php-memcached php-pecl-memcached php-bcmath php-dba php-devel php-embedded php-imap php-intl php-ldap php-mcrypt php-pear php-pspell php-tidy php-xmlrpc php-pecl-zip php-devel php-pecl-imagick php-pecl-imagick-devel`

* After upgrade to PHP 8.1 then re-run the above commands
