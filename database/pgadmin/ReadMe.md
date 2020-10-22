[How To Install pgAdmin4 On CentOS 8](https://sysadminjournal.com/how-to-install-pgadmin4-on-centos-8/)<br />
[PostgreSQL Download](https://download.postgresql.org/pub/repos/yum/reporpms/EL-8-x86_64/)<br />
[Pgadmin 4 RPM](https://www.pgadmin.org/download/pgadmin-4-rpm/)

* `sudo dnf install -y https://download.postgresql.org/pub/repos/yum/reporpms/EL-8-x86_64/pgdg-redhat-repo-latest.noarch.rpm`
* `sudo dnf -qy module disable postgresql`
  * **WAIT FOR THIS TO FINISH**
* `sudo dnf install -y pgadmin4`
  * **WAIT FOR THIS TO FINISH**
* `sudo systemctl restart httpd`
* `sudo systemctl status httpd`
* `sudo cp /etc/httpd/conf.d/pgadmin4.conf.sample /etc/httpd/conf.d/pgadmin4.conf`
  * <pre>
    LoadModule wsgi_module modules/mod_wsgi.so
    WSGIDaemonProcess pgadmin processes=1 threads=25 python-home=/usr/pgadmin4/venv
    WSGIScriptAlias /pgadmin4 /usr/lib/python3.6/site-packages/pgadmin4-web/pgAdmin4.wsgi

    &lt;Directory /usr/lib/python3.6/site-packages/pgadmin4-web/&gt;
      WSGIProcessGroup pgadmin
      WSGIApplicationGroup %{GLOBAL}
      &lt;IfModule mod_authz_core.c&gt;
        # Apache 2.4
        Require all granted
      &lt;/IfModule&gt;
      &lt;IfModule !mod_authz_core.c&gt;
        # Apache 2.2
        Order Deny,Allow
        Deny from All
        Allow from 127.0.0.1
        Allow from ::1
      &lt;/IfModule&gt;
    &lt;/Directory&gt;
    </pre>
* OR
* `sudo cp /etc/httpd/conf.d/pgadmin4.conf.sample /etc/httpd/conf.d/pgadmin4.conf`
  * <pre>
    LoadModule wsgi_module modules/mod_wsgi.so
    WSGIDaemonProcess pgadmin processes=1 threads=25 python-home=/usr/pgadmin4/venv
    WSGIScriptAlias /pgadmin4 /usr/pgadmin4/web/pgAdmin4.wsgi

    &lt;Directory /usr/pgadmin4/web/&gt;
      WSGIProcessGroup pgadmin
      WSGIApplicationGroup %{GLOBAL}
      &lt;IfModule mod_authz_core.c&gt;
        # Apache 2.4
        Require all granted
      &lt;/IfModule&gt;
      &lt;IfModule !mod_authz_core.c&gt;
        # Apache 2.2
        Order Deny,Allow
        Deny from All
        Allow from 127.0.0.1
        Allow from ::1
      &lt;/IfModule&gt;
    &lt;/Directory&gt;
    </pre>
  * This is not needed as of 4.27.# but the above is provided just in case
* `sudo httpd -t` OR `sudo apachectl configtest`
* `sudo systemctl restart httpd`
* `sudo mkdir -p /var/lib/pgadmin4/`
* `sudo mkdir -p /var/log/pgadmin4/`
* `sudo vim /usr/lib/python3.6/site-packages/pgadmin4-web/config_distro.py`
  * <pre>
    HELP_PATH = '/usr/share/doc/pgadmin4-docs/en_US/html'
    UPGRADE_CHECK_ENABLED = False
    </pre>
  * Copy and paste the following to the bottom of the file
    * <pre>
      LOG_FILE = '/var/log/pgadmin4/pgadmin4.log'
      SQLITE_PATH = '/var/lib/pgadmin4/pgadmin4.db'
      SESSION_DB_PATH = '/var/lib/pgadmin4/sessions'
      STORAGE_DIR = '/var/lib/pgadmin4/storage'
      </pre>
  * Save and Exit
* OR
* `sudo vim /usr/pgadmin4/web/config_distro.py`
  * <pre>
    HELP_PATH = '../../../share/docs/en_US/html/'
    DEFAULT_BINARY_PATHS = {
      'pg':   '/usr/bin',
      'ppas': ''
    }
    </pre>
  * Copy and paste the following to the bottom of the file
    * <pre>
      LOG_FILE = '/var/log/pgadmin4/pgadmin4.log'
      SQLITE_PATH = '/var/lib/pgadmin4/pgadmin4.db'
      SESSION_DB_PATH = '/var/lib/pgadmin4/sessions'
      STORAGE_DIR = '/var/lib/pgadmin4/storage'
      </pre>
  * Save and Exit
* `sudo dnf install -y python3-bcrypt python3-pynacl` **NOTE if not already installed**
* `sudo /usr/pgadmin4/web/setup.py`
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
* `sudo rpm -qa | grep pgadmin`

[Local pgAdmin](http://localhost/pgadmin4/)
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
