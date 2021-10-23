[Install Jellyfin Media Server On CentOS Linux](https://computingforgeeks.com/install-jellyfin-media-server-on-centos-linux/)<br />
[Jellyfin And Nginx Configuration](https://jellyfin.org/docs/general/networking/nginx.html)<br />
[List Open Ports Firewalld](https://linuxhint.com/list_open_ports_firewalld/)<br />

* Dependencies to install Jellyfin Media Server is [ffmpeg](https://github.com/Cuates/centosinstall/blob/master/additionalpackage/ffmpeg)
* Visit the following website [Jellyfin for CentOS](https://repo.jellyfin.org/releases/server/centos/stable/) to download the 2 different rpms for the server and web
  * Wget or manually download the rpms
    * Jellyfin server
      * `wget https://repo.jellyfin.org/releases/server/centos/stable/server/jellyfin-server-10.7.7-1.el7.x86_64.rpm`
    * jellyfin-web
      * `wget https://repo.jellyfin.org/releases/server/centos/stable/web/jellyfin-web-10.7.7-1.el7.noarch.rpm`
    * Or manually download both rpms from the Jellyfin CentOS stable list
* Install the downloaded packages
  * Jellyfin-server
    * `sudo dnf -y localinstall jellyfin-server-*.rpm`
  * Jellyfin-web
    * `sudo dnf -y localinstall jellyfin-web-*.rpm`
* Start Jellyfin service
  * `sudo systemctl start jellyfin`
* Enable Jellyfin service
  * `sudo systemctl enable jellyfin`
* Check if Jellyfin service has started successfully
  * `sudo systemctl status jellyfin`
* Your media server is now running and should be accessible via
  * http://server-IP:8096.
* Open port 8096 through firewall router
* Configure Firewall
  * `sudo firewall-cmd --list-ports`
  * `sudo firewall-cmd --zone=public --permanent --add-port=8096/tcp`
* Reload Firwall
  * `sudo firewall-cmd --reload`
* Check Firewall
  * `sudo firewall-cmd --info-service jellyfin`
  * `sudo firewall-cmd --list-ports`
  * `sudo firewall-cmd --list-all`
* Check If Jellyfin Is Running On Port 8096
  * `sudo netstat -pnltu | grep -i 8096`
* Make Sure Router Port Forwards to Port 8096 for Jellyfin Media Server
* Make Sure you Create a jellyfin.example.com Host Name Before Proceeding with Nginx Configuration
* Make Sure Nginx is Installed and Configured on the Linux Server
* Create Nginx Virtual Host Configuration
  * `sudo vim /etc/nginx/conf.d/jellyfinservername.hostname.conf`
  * Add the Following
    * <pre>
        server {
            listen 80;
            listen [::]:80;
            server_name DOMAIN_NAME;

            # use a variable to store the upstream proxy
            # in this example we are using a hostname which is resolved via DNS
            # (if you aren't using DNS remove the resolver line and change the variable to point to an IP address e.g `set $jellyfin 127.0.0.1`)
            set $jellyfin jellyfin;
            resolver 127.0.0.1 valid=30;

            # Security / XSS Mitigation Headers
            add_header X-Frame-Options "SAMEORIGIN";
            add_header X-XSS-Protection "1; mode=block";
            add_header X-Content-Type-Options "nosniff";

            # Content Security Policy
            # See: https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP
            # Enforces https content and restricts JS/CSS to origin
            # External Javascript (such as cast_sender.js for Chromecast) must be whitelisted.
            #add_header Content-Security-Policy "default-src https: data: blob: http://image.tmdb.org; style-src 'self' 'unsafe-inline'; script-src 'self' 'unsafe-inline' https://www.gstatic.com/cv/js/sender/v1/cast_sender.js https://www.youtube.com blob:; worker-src 'self' blob:; connect-src 'self'; object-src 'none'; frame-ancestors 'self'";

            location = / {
                return 302 https://$host/web/;
            }

            location / {
                # Proxy main Jellyfin traffic
                proxy_pass http://$jellyfin:8096;
                proxy_set_header Host $host;
                proxy_set_header X-Real-IP $remote_addr;
                proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
                proxy_set_header X-Forwarded-Proto $scheme;
                proxy_set_header X-Forwarded-Protocol $scheme;
                proxy_set_header X-Forwarded-Host $http_host;

                # Disable buffering when the nginx proxy gets very resource heavy upon streaming
                proxy_buffering off;
            }

            # location block for /web - This is purely for aesthetics so /web/#!/ works instead of having to go to /web/index.html/#!/
            location = /web/ {
                # Proxy main Jellyfin traffic
                proxy_pass http://$jellyfin:8096/web/index.html;
                proxy_set_header Host $host;
                proxy_set_header X-Real-IP $remote_addr;
                proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
                proxy_set_header X-Forwarded-Proto $scheme;
                proxy_set_header X-Forwarded-Protocol $scheme;
                proxy_set_header X-Forwarded-Host $http_host;
            }

            location /socket {
                # Proxy Jellyfin Websockets traffic
                proxy_pass http://$jellyfin:8096;
                proxy_http_version 1.1;
                proxy_set_header Upgrade $http_upgrade;
                proxy_set_header Connection "upgrade";
                proxy_set_header Host $host;
                proxy_set_header X-Real-IP $remote_addr;
                proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
                proxy_set_header X-Forwarded-Proto $scheme;
                proxy_set_header X-Forwarded-Protocol $scheme;
                proxy_set_header X-Forwarded-Host $http_host;
            }
        }
      </pre>
    * Save and exit
* Check Nginx for Syntax Errors
  * `sudo nginx -t`
* Restart Nginx
  * `sudo systemctl restart nginx`
* Check Nginx Status
  * `sudo systemctl status nginx`
* Execute Certbot for HTTPS
  * `sudo certbot --nginx`
* Access Jellyfin Media Server Via Web UI
  * http://jellyfin.example.com
* Configure Jellyfin Media server
  * Open the web interface and configure initial setup
    * Setup Admin user acount
    * Login with your admin credentials you created in the step above.
    * You will be required to setup your media library, choosing the type of media you want to stream and setting up of the content directories.
    * Setup your media system and add content to the jellyfin server in the folders you specified
    * Click Add Media Library to add a different Library then Next
    * Check the Allow remote connections box to allow connections from remote devices.
    * You will then be redirected to the dashboard where you can now see the media that you have uploaded to the folders appear.
    * Content metadata such as banners, Movie information including Cast Crew and ratings will be downloaded automatically (If available).
