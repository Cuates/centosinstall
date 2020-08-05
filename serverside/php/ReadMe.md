[Install LAMP Stack CentOS 8 Rhel 8](https://www.linuxbabe.com/redhat/install-lamp-stack-centos-8-rhel-8)<br />
[How To Install PHP On CentOS 8](https://linuxize.com/post/how-to-install-php-on-centos-8/)<br />
[How To Install PHP 73 On Rhel 8](https://www.itzgeek.com/how-tos/linux/centos-how-tos/how-to-install-php-7-3-on-rhel-8.html)<br />
[Linux Installation](https://www.scriptcase.net/docs/en_us/v9/manual/02-scriptcase-installation/06-linux_php/)
* Remi has to be enabled before the following can be done
  * [Remi Installation and Configuration](https://github.com/Cuates/lampcentosinstall/tree/master/system/remi)
* `sudo dnf module -y enable php:remi-7.4`
* `sudo dnf install -y php php-cli php-common php-curl php-fpm php-mysql php-mysqlnd php-opcache php-gd php-xml php-mbstring php-pdo php-pdo-dblib php-pgsql php-pecl-rar php-odbc php-memcached php-pecl-memcache php-bcmath php-dba php-devel php-embedded php-imap php-intl php-ldap php-mcrypt php-pear php-recode php-pspell php-tidy php-xmlrpc`
* `sudo systemctl start php-fpm`
* `sudo systemctl enable php-fpm`
* `sudo systemctl status php-fpm`
* `sudo systemctl restart httpd`
* `sudo setsebool -P httpd_execmem 1`
* Test with /var/www/html/info.php
  * <?php phpinfo(); ?>
  * Visit website localhost/info.php
  * `sudo rm /var/www/html/info.php` (for security reasons)
* `sudo mkdir /var/log/php`
* `sudo vim /etc/php.ini`
  * serialize_precision = -1
  * max_execution_time = 240
  * date.timezone = America/Los_Angeles
  * error_log = /var/log/php/error.log
* `sudo systemctl restart httpd`
* `sudo apachectl configtest`
* `php -r "echo extension_loaded('zip') ? 'Installed' : 'Not installed';"`
* `php -v`
