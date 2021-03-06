[Install Qbittorrent Centos 8 RHEL 8](https://www.linuxbabe.com/redhat/install-qbittorrent-centos-8-rhel-8)<br />
[How To Instal Qbittorrent On Desktop Server Centos 8 RHEL 8](https://tier4hosting.com/how-to-instal-qbittorrent-on-desktop-server-centos-8-rhel-8/)<br />
[Install qBittorrent Ubuntu 1904 Desktop Server](https://www.linuxbabe.com/ubuntu/install-qbittorrent-ubuntu-19-04-desktop-server)<br />
[Install qBittorrent Webui Ubuntu](https://www.smarthomebeginner.com/install-qbittorrent-webui-ubuntu/)<br />
[Apache SSL FAQ](https://httpd.apache.org/docs/current/ssl/ssl_faq.html#aboutcerts)<br />
[Install qBittorrent Ubuntu 1904 Desktop Server](https://www.linuxbabe.com/ubuntu/install-qbittorrent-ubuntu-19-04-desktop-server)

* Install qBittorrent on CentOS 8/RHEL 8 Server
  * `sudo dnf -y install epel-release`
  * `sudo dnf -y install qbittorrent-nox`
  * `qbittorrent-nox --version`
* Give port permission to qBittorrent Server
  * `sudo firewall-cmd --get-services`
  * `sudo firewall-cmd --zone=public --permanent --add-port=8080/tcp`
  * `sudo firewall-cmd --reload`
  * `sudo firewall-cmd --list-ports`
  * `sudo firewall-cmd --list-all`
* Start qBittorrent-nox
  * `qbittorrent-nox`
    * Press 'y' key and Enter to accept and continue when asked about the Legal Notice
  * Ctrl+C to quit the manual execute
* Web UI accessible Information
  * To control qBittorrent, access the Web UI at http://localhost:8080
  * The Web UI administrator username is: admin
  * The Web UI administrator password is still the default one: adminadmin
  * This is a security risk, please consider changing your password from program preferences.
* Create a qbittorentnox user or utilize an already created user
  * Create a New Group Name for Samba
    * `sudo groupadd <new_group_name>`
  * Associate New User Name to New Group Name
    * `sudo useradd <new_user_name> -G <new_group_name>`
      * A home directory /home/qbittorentnox will be created for this user. Files are downloaded to /home/qbittorrentnox/Downloads/ by default.
  * Associate Existing User to Group
    * `sudo usermod -a -G <new_group_name> <existing_user_name>`
* The qbittorrent-nox package ships with the needed systemd service file
  * Under /usr/lib/systemd/system/ directory you will find qbittorrent-nox@.service
    * Make a copy of the file /usr/lib/systemd/system/qbittorrent-nox@.service to /etc/systemd/system/qbittorrent-nox.service
      * `sudo cp /usr/lib/systemd/system/qbittorrent-nox@.service /etc/systemd/system/qbittorrent-nox.service`
      * Edit the .service file created
        * `sudo vim /etc/systemd/system/qbittorrent-nox.service`
        * Add the user, group, and umask to the template file created above
          * <pre>
            [Unit]
            Description=qBittorrenti-nox service for user qbittorrent-nox
            Documentation=man:qbittorrent-nox(1)
            Wants=network-online.target
            After=network-online.target nss-lookup.target
            
            [Service]
            Type=simple
            PrivateTmp=false
            User=qbittorrentnox
            Group=qbittorrent-nox
            UMask=007
            ExecStart=/usr/bin/qbittorrent-nox
            
            [Install]
            WantedBy=multi-user.target
            </pre>
      * Enable qbittorrent-nox to auto-start at boot time by running the below command
        * `sudo systemctl enable qbittorrent-nox.service`
      * Now we can start the qBittorrent service with the following command
        * `sudo systemctl start qbittorrent-nox.service`
      * Check status
        * `sudo systemctl status qbittorrent-nox.service`
      * If you change the systemd service file, then reload the systemd daemon for the change to take effect
        * `sudo systemctl daemon-reload`
* Access qBittorrent Web UI
  * Open the following in a web browser
    * `<server_ip_address>:8080`
    * Enter in default username and password
      * The default username and password will need to be changed
    * Change username and password
      * Navigate to Tools > Options
        * Select Web UI Tab
          * Under the Authentication section, change both username and password
* Access the library from an external network
  * Navigate to your router's port forward section
    * Add the port to the IP address
