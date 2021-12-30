[Jackett](https://github.com/Jackett/Jackett)<br />
[Jackett Linux Prereqs](https://github.com/dotnet/core/blob/main/Documentation/linux-prereqs.md)

* On most operating systems all the required dependencies will already be present. In case they are not, you can refer to this page https://github.com/dotnet/core/blob/master/Documentation/linux-prereqs.md
  * `sudo dnf install -y libicu`
* Install as service
  * Download and extract the latest Jackett.Binaries.LinuxAMDx64.tar.gz release from the [releases page](https://github.com/Jackett/Jackett/releases)
  * Perform the following command to untar the file if you downloaded the tar.gz
    * `tar xzf /path/to/Jackett.Binaries.LinuxAMDx64.tar.gz`
      * Make sure to untar the file under a non root user
  * To install Jackett as a service
    * Open a Terminal
    * cd to the jackett folder
    * run `sudo ./install_service_systemd.sh`
      * You need root permissions to install the service
      * The service will start on each logon
      * You can always stop it by running `systemctl stop jackett.service` from Terminal
      * You can start it again it using `systemctl start jackett.service`
      * Logs are stored as usual under `~/.config/Jackett/log.txt` and also in `journalctl -u jackett.service`
    * **IMPORTANT NOTE**
      * You need to have a user that is not root assigned within the Jackett service
      * Also, the Jackett folder needs to be accessible to the non root user assigned
    * Make changes to /path/to/services/jackett.service
      * To update any modifications made to jackett.service perform the following command
        * `systemctl daemon-reload`
  * Give port permission to Jackett Server
    * `sudo firewall-cmd --get-services`
    * `sudo firewall-cmd --zone=public --permanent --add-port=9117/tcp`
    * `sudo firewall-cmd --reload`
    * `sudo firewall-cmd --list-ports`
    * `sudo firewall-cmd --list-all`
  * Make Sure Router Port Forwards to Port 9117 for Jackett Server
* Run without installing as a service
  * Download and extract the latest Jackett.Binaries.LinuxAMDx64.tar.gz release from the [releases page](https://github.com/Jackett/Jackett/releases), open a Terminal, cd to the jackett folder and run Jackett with the command `./jackett`
* Home Directory
  * If you want to run it with a user without a /home directory you need to add `Environment=XDG_CONFIG_HOME=/path/to/folder` to your systemd file, this folder will be used to store your config files.
* Running Jackett behind a reverse proxy
  * When running jackett behind a reverse proxy make sure that the original hostname of the request is passed to Jackett. If HTTPS is used also set the X-Forwarded-Proto header to "https". Don't forget to adjust the "Base path override" Jackett option accordingly.
  * Example config for Nginx:
    * <pre>
        location /jackett {
          proxy_set_header X-Real-IP $remote_addr;
          proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
          proxy_set_header X-Forwarded-Proto $scheme;
          proxy_set_header X-Forwarded-Host $http_host;
          proxy_set_header X-Script-Name /jackett;
          proxy_pass http://127.0.0.1:9117;
          proxy_redirect off;
        }
      </pre>
  * Test Nginx
    * `sudo nginx -t`
  * Restart Nginx Service
    * `sudo systemctl restart nginx`
  * Once everything is fine with nginx perform the following on the server IP address and port for Jackett
    * e.g.
      * http://168.17.0.2:9117
    * Modify the Jackett Configuration to work with nginx modifications
      * Base path override:
        * /path/to/base/
          * e.g.
            * /jackett
      * Server port:
        * 9117
      * Optional
        * Add password for secure access to service is not currently working
      * Click on Apply server settings
        * This will refresh the page with the latest modifications
      * Navigate to your URL host name with base path override added to the end
