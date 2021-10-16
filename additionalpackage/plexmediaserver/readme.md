[How To Install Plex Media Server On Centos 8](https://cloudcone.com/docs/article/how-to-install-plex-media-server-on-centos-8/)<br />
[Centos Plex Media Server](https://www.howtoforge.com/tutorial/centos-plex-media-server/)

* Add repository for Plex Media Server on CentOS 8
  * `sudo vim /etc/yum.repos.d/plex.repo`
    * <pre>
        [Plex]
        name=Plex
        baseurl=https://downloads.plex.tv/repo/rpm/$basearch/
        enabled=1
        gpgkey=https://downloads.plex.tv/plex-keys/PlexSign.key
        gpgcheck=1
      </pre>
* `sudo  dnf makecache`
* `sudo dnf clean all`
* Install Plex
  * `sudo dnf install -y plexmediaserver`
* Enable on Boot
  * `sudo systemctl enable plexmediaserver`
* Start Plex Media Server
  * `sudo systemctl start plexmediaserver`
* Check Plex Media Server Status
  * `sudo systemctl status plexmediaserver`
* Configure Firewall
  * `sudo firewall-cmd --get-services`
  * `sudo firewall-cmd --zone=public --permanent --add-service=plex`
* Reload Firwall
  * `sudo firewall-cmd --reload`
* Check Firewall
  * `sudo firewall-cmd --list-services`
  * `sudo firewall-cmd --info-service plex`
  * `sudo firewall-cmd --list-all`
* Congfigure Plex Media Server to be Accessed Over the Internet
  * `sudo setsebool httpd_can_network_connect 1`
  * Does not need to be done if already done during the Nginx/Apache setup process
* Access Plex Media Server Via Web UI
  * http://server-ip:32400/web
* Make Sure Router Port Forwards to Port 32400 for Plex Media Server
* Make Sure you Create a plex.example.com Host Name Before Proceeding with Nginx Configuration
* Make Sure Nginx is Installed and Configured on the Linux Server
* Create Nginx Virtual Host Configuration
  * `sudo vim /etc/nginx/config.d/plex.conf`
  * Add the Following
    * <pre>
        upstream plex_backend {
          server 127.0.0.1:32400;
          keepalive 32;
        }

        server {
          listen 80;
          server_name plex.example.com;

          send_timeout 100m; #Some players don't reopen a socket and playback stops totally instead of resuming after an extended pause (e.g. Ch$

          #Plex has A LOT of javascript, xml and html. This helps a lot, but if it causes playback issues with devices turn it off. (Haven't enc$
          gzip on;
          gzip_vary on;
          gzip_min_length 1000;
          gzip_proxied any;
          gzip_types text/plain text/css text/xml application/xml text/javascript application/x-javascript image/svg+xml;
          gzip_disable "MSIE [1-6]\.";

          #Nginx default client_max_body_size is 1MB, which breaks Camera Upload feature from the phones.
          #Increasing the limit fixes the issue. Anyhow, if 4K videos are expected to be uploaded, the size might need to be increased even more
          client_max_body_size 100M;

          #Forward real ip and host to Plex
          proxy_set_header Host $host;
          proxy_set_header X-Real-IP $remote_addr;
          proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
          proxy_set_header X-Forwarded-Proto $scheme;
          proxy_set_header Sec-WebSocket-Extensions $http_sec_websocket_extensions;
          proxy_set_header Sec-WebSocket-Key $http_sec_websocket_key;
          proxy_set_header Sec-WebSocket-Version $http_sec_websocket_version;
          #Websockets
          proxy_http_version 1.1;
          proxy_set_header Upgrade $http_upgrade;
          proxy_set_header Connection "Upgrade";

          #Buffering off send to the client as soon as the data is received from Plex.
          proxy_redirect off;
          proxy_buffering off;

          location / {
            proxy_pass http://plex_backend;
          }
        }
      </pre>
* Configure Nginx Bucket Size
  * `sudo vim /etc/nginx/nginx.conf`
  * Add the Following at End of File
    * <pre>
        # Define Nginx server hash bucket size
        server_names_hash_bucket_size 64;
      </pre>
* Check Nginx for Syntax Errors
  * `sudo nginx -t`
* Restart Nginx
  * `sudo systemctl restart nginx`
* Check Nginx Status
  * `sudo systemctl status nginx`
* Access Plex Media Server Via Web UI
  * http://plex.example.com
