[How To Install Imagemagick And PHP Imagick On CentOS 8 rhel 8](https://www.itzgeek.com/post/how-to-install-imagemagick-and-php-imagick-on-centos-8-rhel-8/)<br />
[Install Imagemagick CentOS 8](https://idroot.us/install-imagemagick-centos-8/)
* `sudo dnf install -y epel-release`
* `sudo dnf config-manager --set-enabled PowerTools`
* `sudo dnf install -y ImageMagick ImageMagick-devel`
* `sudo dnf install -y php php-devel php-pear make`
* `sudo pecl channel-update pecl.php.net`
* `sudo pecl install imagick`
* `sudo vim /etc/php.d/20-imagick.ini`
  * extension=imagick.so
* `sudo systemctl restart httpd`
* `sudo php -m`
* `convert --version`
