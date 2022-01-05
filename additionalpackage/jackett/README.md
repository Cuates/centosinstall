[Jackett](https://github.com/Jackett/Jackett)<br />
[Jackett Linux Prereqs](https://github.com/dotnet/core/blob/main/Documentation/linux-prereqs.md)<br />
[Jackett MAC OS Issues 5589](https://github.com/Jackett/Jackett/issues/5589)

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
    * run install script
      * `sudo ./install_service_systemd.sh`
       * You need root permissions to install the service
       * The service will start on each logon
       * You can always stop it by running from Terminal
         * `systemctl stop jackett.service`
       * You can start it again it using
         * `systemctl start jackett.service`
       * Logs are stored in the following path file
         * `~/.config/Jackett/log.txt`
       * Logs can also be seen with the following command
         * `journalctl -u jackett.service`
    * **IMPORTANT NOTE**
      * You need to have a user that is not root within the Jackett service
      * Also, the Jackett folder needs to be accessible to the non root user
    * Make changes to /path/to/services/jackett.service
      * To update any modifications made to jackett.service perform the following command
        * `systemctl daemon-reload`
  * Give port permission to Jackett Server
    * Default port for Jacektt server is 9117 
      * `sudo firewall-cmd --get-services`
      * `sudo firewall-cmd --zone=public --permanent --add-port=9117/tcp`
      * `sudo firewall-cmd --reload`
      * `sudo firewall-cmd --list-ports`
      * `sudo firewall-cmd --list-all`
  * Make Sure Router Port Forwards to Port 9117 for Jackett Server
* **OPTIONAL** Run without installing as a service
  * Download and extract the latest Jackett.Binaries.LinuxAMDx64.tar.gz release from the [releases page](https://github.com/Jackett/Jackett/releases)
    * Open a Terminal
    * cd to the jackett folder
    * run Jackett with the following command
      * `./jackett`
* **OPTIONAL** Home Directory
  * If you want to run it with a user without a /home directory you need to add the following to your systemd file
    * `Environment=XDG_CONFIG_HOME=/path/to/folder`
      * This folder will be used to store your config files
* **RECOMMENDED** Running Jackett behind a reverse proxy
  * When running jackett behind a reverse proxy make sure that the original hostname of the request is passed to Jackett. If HTTPS is used also set the X-Forwarded-Proto header to "https"
  * **IMPORTANT** Don't forget to adjust the "Base path override" Jackett option accordingly on the Jackett UI
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
      * [localhost](http://localhost:9117)
    * Modify the Jackett Configuration to work with nginx modifications
      * Base path override:
        * /path/to/base/
          * e.g.
            * /jackett
      * Server port:
        * 9117
      * Optional
        * Add password for secure access to service
          * This is currentlty not working 
      * Click on Apply server settings
        * This will refresh the page with the latest modifications
  * The Jackett UI is now setup when you navigate to your URL host name with base path override added to the end
* MAC OS X Install 
  * Download and extract the latest Jackett.Binaries.macOS.tar.gz release from the [releases page](https://github.com/Jackett/Jackett/releases)
  * Open a terminal of choice
    * Read the quarantine attribute of one dll
      * `xattr -p com.apple.quarantine libhostfxr.dylib`
    * Copy the string (should be something like "0081;5d1bec70;Archive Utility;0622FF31-4499-4EBA-954A-EDC879E4010A") but replace the first 4 characters by 00c1 which tells Gatekeeper to shut up. Then use your modified string:
      * e.g.
        * `xattr -w com.apple.quarantine "00c1;5d1bec70;Archive Utility;0622FF31-4499-4EBA-954A-EDC879E4010A" *.{dylib,dll}`
      * This will effectively whitelist all the dll and dylib files, allowing Jackett to run.
    * Run Jackett without installing as a service using the following command
      * `./jackett`
    * Open site on the following http
      * [localhost](http://localhost:9117)
    * Shut down application use the following command in the terminal
      * `Ctrl+C `
