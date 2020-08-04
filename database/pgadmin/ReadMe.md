[How To Install pgAdmin4 On CentOS 8](https://sysadminjournal.com/how-to-install-pgadmin4-on-centos-8/)<br />
[PostgreSQL Download](https://download.postgresql.org/pub/repos/yum/reporpms/EL-8-x86_64/)
* `sudo dnf install -y https://download.postgresql.org/pub/repos/yum/reporpms/EL-8-x86_64/pgdg-redhat-repo-latest.noarch.rpm`
* `sudo dnf -qy module disable postgresql`
  * **WAIT FOR THIS TO FINISH**
* `sudo dnf install -y pgadmin4`
  * **WAIT FOR THIS TO FINISH**
* `sudo systemctl restart httpd`
* `sudo systemctl status httpd`
* `sudo cp /etc/httpd/conf.d/pgadmin4.conf.sample /etc/httpd/conf.d/pgadmin4.conf`
* `sudo httpd -t OR sudo apachectl configtest`
* `sudo systemctl restart httpd`
* `sudo mkdir -p /var/lib/pgadmin4/`
* `sudo mkdir -p /var/log/pgadmin4/`
* `sudo vim /usr/lib/python3.6/site-packages/pgadmin4-web/config_distro.py`
  * LOG_FILE = '/var/log/pgadmin4/pgadmin4.log'
  * SQLITE_PATH = '/var/lib/pgadmin4/pgadmin4.db'
  * SESSION_DB_PATH = '/var/lib/pgadmin4/sessions'
  * STORAGE_DIR = '/var/lib/pgadmin4/storage'
* `sudo dnf install -y python3-bcrypt python3-pynacl`
* `sudo python3 /usr/lib/python3.6/site-packages/pgadmin4-web/setup.py`
  * Email address: admin@example.com
  * Password: PASSWORD_HERE
  * Retype password
* `sudo chown -R apache:apache /var/lib/pgadmin4`
* `sudo chown -R apache:apache /var/log/pgadmin4`
* `sudo chcon -t httpd_sys_rw_content_t /var/lib/pgadmin4 -R`
* `sudo chcon -t httpd_sys_rw_content_t /var/log/pgadmin4 -R`
* `sudo setsebool -P httpd_can_network_connect 1`
* `sudo setsebool -P httpd_can_network_connect_db 1`
* `sudo firewall-cmd --add-service={http,https} --permanent`
* `sudo firewall-cmd --reload`
* `sudo systemctl restart httpd`

[Local pgAdmin](http://server-ip/pgadmin4/)
* username
* password
* Add New Server
  * Host name/address
  * Port
  * Maintenance Database
  * Username of PostgreSQL
  * Password of PostgreSQL
  * Save password?
    * Check
  * Click: 'Save' button
    * Automatically connects to your PostgreSQL server
  * sudo rpm -qa | grep pgadmin
