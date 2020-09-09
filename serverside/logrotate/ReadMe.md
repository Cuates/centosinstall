[How To Debug Logrotate Warnings Or Errors](https://access.redhat.com/solutions/32831)
* `sudo mkdir /var/log/php`
* `sudo vim /etc/logrotate.d/php`
  * /var/log/php/*log {<br />
    missingok<br />
    notifempty<br />
    sharedscripts<br />
    delaycompress<br />
    postrotate<br />
        /bin/systemctl reload httpd.service > /dev/null 2>/dev/null || true<br />
    endscript<br />
    }
* `sudo systemctl restart rsyslog`
* `sudo logrotate --force -v /etc/logrotate.d/php`
* `sudo /usr/sbin/logrotate -d /etc/logrotate.conf`

**IMPORTANT NOTE**
* Utilized with PHP-FPM instead
