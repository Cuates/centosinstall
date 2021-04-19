[Install PHP 73 fpm Remirepo On CentOS](https://blog.kerus.net/1014/install-php-7-3-fpm-remirepo-on-centos)<br />
[Install Memcached En PHP Memcache](https://www.unixmen.com/install-memcached-en-php-memcache/)
* `sudo dnf install -y memcached`
* `sudo vim /etc/sysconfig/memcached`
  * WAS
    * <pre>
      CACHESIZE="64"
      </pre>
  * IS
    * <pre>
      CACHESIZE="2048"
      </pre>
  * WAS
    * <pre>
      OPTIONS="-l 127.0.0.1,::1"
      </pre>
  * IS
    * <pre>
      OPTIONS=""
      </pre>
* `sudo chkconfig --levels 235 memcached on`
* `sudo systemctl start memcached`
* `sudo systemctl enable memcached`
* `sudo systemctl status memcached`
* `sudo netstat -an | grep 11211`
* `sudo memcached-tool localhost:11211 stats`
* `sudo systemctl restart httpd`
* OR
* `sudo systemctl restart nginx`
* `memcached --version`
