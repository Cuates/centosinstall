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

* Set up the setting for qBittorrent
  ** These are based on Windows application settings **
  * Behavior
    * Interface
      * Language
        * English
    * Transfer List
      * Check
        * Confirm when deleting torrents
        * Use alternating row colors
    * Desktop
      * Check
        * Confirmation on auto-exit when downloads finish
          * Show qBittorrent in notification area
          * Minimize qBittorrent in notification area
          * Close qBittorrent to notification area
          * Tray icon style
            * Select
              * Monochrome (for dark theme)
          * File association
            * Use qBittorrent for .torrent file
            * Use qBittorrent for magnet links
        * Check for program update
    * Power Management
      * Check
        * Inhibit system sleep when torrents are downloading
        * Inhibit system sleep when torrents are seeding 
    * Log File
      * Check
        * Backup the log file after 65 KiB
        * Delete backup logs folder older than 1 months
  * Downloads
    * When adding a torrent
      * Check
        * Display torrent content and some options
        * Bring torrent dialog to the front
    * Check
      * Enable recursive download dialog
    * Saving Management
      * Default Save Path
        * Browse
          * <path_to_torrent_directory>
  * Connections
    * Peer Connection Protocol
      * Select
        * TCP and muTP
    * Listening Port
      * Port used for incoming connections
        * Choose any port you like or leave as default
      * Check
        * Use UPnP / NAT-PMP port forwarding from my router
    * Connection Limits
      * Check
        * Global maximum number of connections
          * Choose number of connection
            * i.e. 500
            * **Note** If you set this value higher than your connection speed may vary
        * Global maximum number of connections per torrent
          * Choose number of connection
            * i.e. 100
            * **Note** If you set this value higher than your connection speed may vary
        * Global maximum number of upload slots
          * Choose number of connection
            * i.e. 1
            * **Note** If you set this value higher than your connection speed may vary
        * Global maximum number of upload slots per torrent
          * Choose number of connection
            * i.e. 1
            * **Note** If you set this value higher than your connection speed may vary
  * Speed
    * Global Rate Limits
      * Upload
        * Select
          * i.e. 10 KiB/s
      * Download
        * Select
          * i.e. (infinity)
    * Alternative Rate Limits
      * Upload
        * Select
          * i.e. 10 KiB/s
      * Download
        * Select
          * i.e. (infinity)
    * Rate Limits Setting
      * Check
        * Apply rate limit to muTP protocol
        * Apply rate limit to peers on LAN
  * BitTorrent
    * Privacy
      * Check
        * Enable DHT (decentralized network) to find more peers
        * Enable peer exchange (PeX) to find more peers
        * Encryption Mode
          * Select
            * Require encryption
        * Enable anomymous mode
    * Maximum Active Checking Torrents
      * Select
        * i.e. 1
        * **Note** If you set this value higher than your connection speed may vary
    * Torrent Queueing
      * Maximum Active Downloads
        * Choose number in queue
         * i.e. (Infinity)
         * **Note** Your connection speed may vary
      * Maximum Active Uploads
       * Choose number in queue
        * i.e. 1
        * **Note** If you set this value higher than your connection speed may vary
      * Maximum Active Torrents
        * Choose number in queue
         * i.e. (Infinity)
         * **Note** Your connection speed may vary
      * Check
        * Do not count slow torrents in these limits
      * Download rate threshold
        * Choose number
          * i.e. 10 KiB/s
          * **Note** Your connection speed may vary
      * Upload rate threshold
        * Choose number
          * i.e. 10 KiB/s
          * **Note** If you set this value higher than your connection speed may vary
      * Torrent inactivity timer
        * Choose number
          * i.e. 60 sec
          * **Note** Your connection speed may vary
    * Seeding Limits
      * Check
        * When ratio reaches
          * Choose
            * i.e. 1.00
            * Then choose
              * Pause torrent
  * RSS
    * Leave as default
  * Web UI
    * **NOTE** Only configure if you are going to use the UI
    * Check
      * Web user interface (Remote control)
        * IP Address
          * Input asterisk (*)
          * Choose
            * Port number
              * **NOTE** The port number will be provided or you can choose one
          * Authentication
            * Username
              * i.e. username if any
            * Password
              * i.e. password if any
            * Check
              * Bypass authentication for clients on localhost
          * Security
            * Check
              * Enable clickjacking protection
              * Enable cross-site request forgery (CSRF) proection
              * Enable host header validation
                * Server Domain
                  * Input asterisk (*) 
  * Advanced
    * Confirm Torrent Recheck
      * Check
    * Refresh Interval
      * i.e. 1500 ms
    * Asynchronous I/O threads
      * i.e. 10
    * File Pool Size
      * i.e. 40
    * Outstanding memory when checking torrents
      * i.e. 32 MiB
    * Disk Cache **NOTE** Not on new version
      * i.e. -1 (auto)
    * Dish Cache Expiry Interval **NOTE** Not on new version
      * i.e. 60 s
    * Disk Queue Size
      * i.e. 1024 KiB
    * Outgoing Connections Per Second
      * i.e. 30
    * Socket Backlog Size
      * i.e. 30
    * Outgoing Ports (min) [0: disable]
      * i.e. 0
    * Outgoing Ports (max) [0: disable]
      * i.e. 0
    * Type of Service (ToS) for connections to peers
      * i.e. 4
    * muTP-TCP mix mode algorithnm
      * Choose
        * i.e. Prefer TCP
    * Validate HTTPS tracker certificates
      * Check
    * Server-side requests forgery (SSRF) mitigation
      * Check
    * Upload Slot Behavior
      * Choose
        * i.e. Fixed slots
    * Upload Choking Algorthim
      * Choose
        * i.e. Fastest upload
    * Always announce to all tiers
      * Check
    * Max concurrent http announces
      * i.e. 50
    * Stop tracker timeout
      * i.e. 5 s
    * Peer Turnover diconnect percentage
      * i.e. 4 %
    * Peer Turnover threshold percentage
      * i.e. 90 %
    * Peer Turnover diconnect interval
      * i.e. 300 s
    * Maximum outstandin request to a single peer
      * i.e. 500
