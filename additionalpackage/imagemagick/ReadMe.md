[How To Install Imagemagick And PHP Imagick On CentOS 8 rhel 8](https://www.itzgeek.com/post/how-to-install-imagemagick-and-php-imagick-on-centos-8-rhel-8/)<br />
[Install Imagemagick CentOS 8](https://idroot.us/install-imagemagick-centos-8/)<br />
[How To Enable PowerTools Repository In CentOS 8](https://serverfault.com/questions/997896/how-to-enable-powertools-repository-in-centos-8)

* `sudo dnf install -y epel-release`
* `sudo dnf config-manager --set-enabled powertools`
  * **NOTE** Do not need this command any more
* `sudo dnf repolist`
* `sudo dnf install -y ImageMagick ImageMagick-devel`
* `sudo dnf install -y php php-devel php-pear make`
* `sudo pecl channel-update pecl.php.net`
* `sudo pecl install imagick`
  * Please provide the prefix of ImageMagick installation [autodetect]: Enter
    * **WAIT FOR THIS TO FINISH**
* Open the following file and add the lines to the file **NOTE: If not already present**
  * `sudo vim /etc/php.d/40-imagick.ini`
    * <pre>
      ; Enable imagick extension module
      extension = imagick.so

      ; Documentation: http://php.net/imagick

      ; Don't check builtime and runtime versions of ImageMagick
      imagick.skip_version_check=1

      ; Fixes a drawing bug with locales that use ',' as float separators.
      ; imagick.locale_fix=0

      ; Used to enable the image progress monitor.
      ; imagick.progress_monitor=0
      </pre>
  * Save and Exit
* `sudo systemctl restart httpd`
* * OR
* `sudo systemctl restart nginx`
* `sudo php -m`
* `convert --version`
