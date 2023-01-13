[Install postgresql and pgadmin rhel 9](https://www.tecmint.com/install-postgresql-and-pgadmin-rhel-9/)<br />
[pgadmin 4 rpm](https://www.pgadmin.org/download/pgadmin-4-rpm/)<br />
[Pgadmin4 Installation - Craines](https://gist.github.com/craines/ba6fe9ba416df841d8e5ac5da6128ea7)<br />
[Install Pgadmin4](https://gist.github.com/rubinhozzz/368176fec80edcf449a76e15164ff728)<br />
[Nginx Pgadmin](https://github.com/rbernardes/nginx-pgadmin)<br />
[Pgadmin4 4.28 Py3 None Any Wheel](https://ftp.postgresql.org/pub/pgadmin/pgadmin4/v4.28/pip/pgadmin4-4.28-py3-none-any.whl)<br />
[Pgadmin4](https://ftp.postgresql.org/pub/pgadmin/pgadmin4/)<br />
[Django Nginx Emerg Open Etc Nginx Proxy Params Failed 2 No Such File](https://stackoverflow.com/questions/42589781/django-nginx-emerg-open-etc-nginx-proxy-params-failed-2-no-such-file)<br />
[Server Deployment](https://www.pgadmin.org/docs/pgadmin4/latest/server_deployment.html)<br />
[Pgadmin 4 Python](https://www.pgadmin.org/download/pgadmin-4-python/)<br />
[Pgadmin4 Installation - Rubinhozzz](https://gist.github.com/rubinhozzz/9217e8b0dc834874a301cd0435e70691)<br />
[How To Set Up Pgadmin4 With Nginx In Ubuntu 16.04](https://askubuntu.com/questions/939881/how-to-set-up-pgadmin4-with-nginx-in-ubuntu-16-04)<br />
[Nginx Configure Pgadmin In Location](https://stackoverflow.com/questions/45958416/nginx-configure-pgadmin-in-location)<br />
[Install pgadmin rocky linux almalinux](https://www.tecmint.com/install-pgadmin-rocky-linux-almalinux/)<br />

* **IMPORTANT NOTE Make sure to be root user**
* **The following was executed with `python3.10` and `pip3.10`**

* Download wheel (last version)
  * Note will need to get the latest one from the web site
    * `cd ~`
    * `wget https://ftp.postgresql.org/pub/pgadmin/pgadmin4/v6.18/pip/pgadmin4-6.18-py3-none-any.whl`
* Create /opt/pgadmin4 folder
  * `sudo mkdir /opt/pgadmin4`
* Create and activate virtual environment
  * `cd /opt`
  * `python3.11 -m venv /opt/pgadmin4`
  * `cd /opt/pgadmin4`
  * `source bin/activate`
* Copy the downloaded .wheel to /opt/pgadmin4 and install
  * `cp ~/pgadmin4-6.18-py3-none-any.whl /opt/pgadmin4/`
  * `pip3.11 install pgadmin4-X.X-py2.py3-none-any.whl`
    * NOTE X.X is the latest version number
    * * WAIT FOR THIS TO FINISH
* Create data directory
  * `mkdir data`
* Create a config_local.py file inside the following directory
  * `cd /opt/pgadmin4/lib/python3.11/site-packages/pgadmin4`
  * `sudo vim /opt/pgadmin4/lib/python3.11/site-packages/pgadmin4/config_local.py`
    * Paste the following into the file
      <pre>
      import os

      DATA_DIR = os.path.realpath(os.path.expanduser(u'/opt/pgadmin4/data/'))
      LOG_FILE = os.path.join(DATA_DIR, 'pgadmin4.log')
      SQLITE_PATH = os.path.join(DATA_DIR, 'pgadmin4.db')
      SESSION_DB_PATH = os.path.join(DATA_DIR, 'sessions')
      STORAGE_DIR = os.path.join(DATA_DIR, 'storage')
      </pre>
    * Save and exit
* Run setup to install pgadmin4
  * Note: Initial setup will ask for e-mail and password.
  * `python3.11 /opt/pgadmin4/lib/python3.11/site-packages/pgadmin4/pgAdmin4.py`
    * Following output was displayed
      <pre>
      pgAdmin 4 - Application Initialisation
      ======================================

      Starting pgAdmin 4. Please navigate to http://127.0.0.1:5050 in your browser.
      * Serving Flask app "pgadmin" (lazy loading)
      * Environment: production
        WARNING: Do not use the development server in a production environment.
        Use a production WSGI server instead.
      * Debug mode: off
      </pre>
    * Enter username and password if asked
    * CRTL+C to quit from the pgadmin installation
* Install gunicorn
  * `cd /opt/pgadmin4`
  * `pip3.11 install gunicorn`
  * `deactivate`
* Create and run pgadmin4.service for systemd
  * `cd /etc/systemd/system/`
  * `sudo vim pgadmin4.service`
    * Paste the following into the file
      ** Note the bind ip and port number can change to whatever you need it to be **
      <pre>
      [Unit]
      Description=pgAdmin4 service
      After=network.target

      [Service]
      User=root
      Group=root
      Environment="PATH=/opt/pgadmin4/bin"
      ExecStart=/opt/pgadmin4/bin/gunicorn --bind 127.0.0.1:5050 --workers=1 --threads=25 --chdir /opt/pgadmin4/lib/python3.10/site-packages/pgadmin4 pgAdmin4:app

      [Install]
      WantedBy=multi-user.target
      </pre>
    * Save and exit
* Start the pgadmin4 service:
  * Reload any modifications to the service file
    * `sudo systemctl daemon-reload`
  * Start the service
    * `sudo systemctl start pgadmin4.service`
  * Stop the service from running
    * `sudo systemctl stop pgadmin4.service`
  * Enable the service to start on startup (boot up)
    * `sudo systemctl enable pgadmin4.service`
  * Disable the service from starting on startup (boot up)
    * `sudo systemctl disable pgadmin4.service`
  * Check the status of the service
    * `sudo systemctl status pgadmin4.service`
* Add pgadmin4 to the Nginx configuration file
  * ** Make sure to find your conf that you are utilizing for your web service **
    * `cd /etc/nginx/conf.d`
    * `sudo vim /etc/nginx/conf.d/cuateslws.ddns.net.conf`
      * Paste the following within the main server block of code in the file
        <pre>
        location /pgadmin4 {
          proxy_set_header Host $http_host;
          proxy_set_header X-Real-IP $remote_addr;
          proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
          proxy_set_header X-Forwarded-Proto $scheme;
          proxy_set_header X-Script-Name /pgadmin4;
          proxy_pass http://127.0.0.1:5050;
        }
        </pre>
      * Save and exit
* Reload nginx
  * `sudo nginx -t`
  * `sudo systemctl reload nginx.service`
* Configure the firewall to see the new port number
  * `sudo firewall-cmd --get-services`
  * `sudo firewall-cmd --zone=public --permanent --add-port=5050/tcp`
  * `sudo firewall-cmd --reload`
  * `sudo firewall-cmd --list-ports`
  * `sudo firewall-cmd --list-all`
  * Optional Step
    * Open port through your router via port forwarding
* Additional Commands (Optional)
  * See if gunicorn is running
    * `ps aux | grep gunicorn`
  * See information about your service
    * `sudo systemctl list-unit-files | grep pgadmin4`
  * See if your service is active
    * `sudo systemctl is-active pgadmin4`
