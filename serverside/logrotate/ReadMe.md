[How To Debug Logrotate Warnings Or Errors](https://access.redhat.com/solutions/32831)

**OPTIONAL This can be left out as we are using php-fpm instead**
* `sudo mkdir /var/log/php`
* `sudo vim /etc/php.ini`
  * <pre>
    error_log = /var/log/php/error.log
    </pre>
* `sudo vim /etc/logrotate.d/php`
  * <pre>
    /var/log/php/*log {
    missingok
    notifempty
    sharedscripts
    delaycompress
    postrotate
        /bin/systemctl reload httpd.service &gt; /dev/null 2&gt;/dev/null || true
    endscript
    }
    </pre>
* `sudo systemctl restart rsyslog`
* `sudo logrotate --force -v /etc/logrotate.d/php`
* `sudo /usr/sbin/logrotate -d /etc/logrotate.conf`

**IMPORTANT NOTE**
* Utilized with PHP-FPM instead
