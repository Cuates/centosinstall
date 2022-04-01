[How To Install PHP 73 On rhel 8](https://www.itzgeek.com/how-tos/linux/centos-how-tos/how-to-install-php-7-3-on-rhel-8.html)
* Version 8
  * `sudo rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm`
  * `sudo dnf install -y https://rpms.remirepo.net/enterprise/remi-release-8.rpm`
* Version 9
  * `sudo rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-9.noarch.rpm`
  * `sudo dnf install -y https://rpms.remirepo.net/enterprise/remi-release-9.rpm`
* `sudo rpm -qa | grep remi-release`
