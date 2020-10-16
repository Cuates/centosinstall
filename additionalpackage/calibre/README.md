[How To Create A Calibre eBook Server On Ubuntu 20.04](https://www.digitalocean.com/community/tutorials/how-to-create-a-calibre-ebook-server-on-ubuntu-20-04)
[Calibre eBook Download Linux](https://calibre-ebook.com/download_linux)
[Calibre Server on Linux](https://gist.github.com/plembo/337f323e53486cbdb03100692ae8c892)
[Calibre Server Calibre Content Server Linux CLI WEBUI](https://www.youtube.com/watch?v=N1hwEfa9W1s)
[Calibre Using A Full Virtual Host](https://manual.calibre-ebook.com/server.html#using-a-full-virtual-host)
[Calibre Managing User Accounts From The Command Line Only](https://manual.calibre-ebook.com/server.html#managing-user-accounts-from-the-command-line-only)
[Calibre Server](https://manual.calibre-ebook.com/generated/en/calibre-server.html)
[calibre-is-awesome-calibreerver Is Not](https://grantwinney.com/calibre-is-awesome-calibre-server-is-not/)
[Service Names Port Numbers](https://www.iana.org/assignments/service-names-port-numbers/service-names-port-numbers.xhtml?&page=86)
[Gutenberg](https://www.gutenberg.org/)
[Remove Files Directories](https://linuxhandbook.com/remove-files-directories/)
[Calibre Add Password In File](https://www.mobileread.com/forums/showthread.php?p=3645101)
[Calibre DB Commands](https://manual.calibre-ebook.com/generated/en/calibredb.html#id1)

* Visit the IANA web site for unassigned ports
  * List Of Some Unassigned Ports
    * 4805 - 4826

* Create a new user
  * `sudo useradd <new_user_name>`
* Create a Calibre Folder
  * `sudo mkdir -p /path/to/calibre/folder`
    * The folder can be named differently for different library names (http://your_server_ip:4805 containing different port numbers if there are multiple calibre servers)
    * At this time there is no way to execute multiple calibre servers simultaneously on a Linux server
* Change owner
  * `sudo chown -R <new_user_name>:<new_user_name> /path/to/calibre/folder`
* Provide permission to the calibre user
  * `sudo chmod ugo+w /path/to/calibre/folder`

* Binary Install
  * `sudo -v && wget -nv -O- https://download.calibre-ebook.com/linux-installer.sh | sudo sh /dev/stdin`
  * If you get an error about an untrusted certificate, that means your computer does not have any root certificates installed and so cannot download the installer securely. If you still want to proceed, pass the --no-check-certificate option to wget, like this:
    * `sudo -v && wget --no-check-certificate -nv -O- https://download.calibre-ebook.com/linux-installer.sh | sudo sh /dev/stdin`
    * `calibre-server --version`
  * If you want to upgrade **IMPORTANT NOTE Every time you update you lose user accounts and libraries if no sqlitedb has been created**
    * `sudo systemctl stop calibre-server.service`
    * `sudo -v && wget -nv -O- https://download.calibre-ebook.com/linux-installer.sh | sudo sh /dev/stdin`
  * If you want to uninstall
    * `/usr/bin/calibre-uninstall`
* Run the following command to download this book to your server
  * `sudo wget http://www.gutenberg.org/ebooks/46.kindle.noimages -O christmascarol.mobi`
* And add the book you just downloaded to your new library using the calibredb command:
  * `calibredb add *.mobi --with-library /path/to/calibre/library_name`
* Give port permission to Calibre Server (Open as many ports as there are calibre servers)
  * `sudo firewall-cmd --get-services`
  * `sudo firewall-cmd --zone=public --permanent --add-port=4805/tcp`
    * **This may need to be done multiple times with different ports per calibre server**
  * `sudo firewall-cmd --reload`
  * `sudo firewall-cmd --list-ports`
  * `sudo firewall-cmd --list-all`
* Now run the following command to start the calibre content server
  * `calibre-server --port=4805 /path/to/calibre/library_name`
  * From your local machine, visit your_server_ip:4805 (substituting your server’s IP address) and you will see the default calibre screen. Click on calibre-library and you will see the book that you added in the previous step.
  * Ctrl+C to stop the manual server process
* Creating a Service for the calibre Content Server
  * To improve the usability of the calibre Content server, let’s replace our manual server process with a service that will start on boot.
  * First, create a file called calibre-server.service in the directory /etc/sytemd/system/
    * `sudo vim /etc/systemd/system/calibre-server.service`
    * Now add the following configurations, which will start the calibre Content server on boot. Make sure to replace the highlighted text with your user and group
      * `## startup service`
        `[Unit]`
        `Description=calibre content server`
        `After=network.target`
        `[Service]`
        `Type=simple`
        `User=<new_user_name>`
        `Group=<new_user_name>`
        `ExecStart=/opt/calibre/calibre-server --port=4805 /path/to/calibre/library_name --enable-local-write`
        `[Install]`
        `WantedBy=multi-user.target`
    * Save and close the file
    * Now enable the service to start on boot up and start it
      * `sudo systemctl enable calibre-server`
      * `sudo systemctl start calibre-server`
    * Reboot your server to test if the new calibre-server booted automatically
      * `sudo shutdown -r now`
      * Wait a few minutes and then visit http://your_server_ip:4805 again in your local web browser to ensure that the calibre Content server booted automatically.
* Adding User Authentication to the calibre Content Server
  * `sudo systemctl stop calibre-server`
  * Now start calibre’s user management sqlitedb script
    * `calibre-server --userdb /path/to/calibre/useraccount/users.sqlite --manage-users`
    * When prompted, choose to add a new user. Then select a username and strong password.
    * Execute command again and set library permissions as well
  * Now we need to make another edit to our service
    * Reopen service file created earlier
      * ***IMPORTANT NOTE***
        * <new_user_name> must have root or sudoer privileges
      * `sudo vim /etc/systemd/system/calibre-server.service`
        * `## startup service`
          `[Unit]`
          `Description=calibre content server`
          `After=network.target`
          `[Service]`
          `Type=simple`
          `User=<new_user_name>`
          `Group=<new_user_name>`
          `ExecStart=/opt/calibre/calibre-server --port=4805 --userdb /path/to/calibre/useraccount/users.sqlite --enable-auth /path/to/calibre/library_name --enable-local-write`
          `[Install]`
          `WantedBy=multi-user.target`
      * Save and close the file
    * Refresh the services daemon to rescan the services files, and start the calibre server again with
      * `sudo systemctl daemon-reload`
      * `sudo systemctl start calibre-server`
      * If you visit your library again, it should now prompt you for a username and password before allowing you to access it.
      * If you get something along the lines of the below message, then clear your browser cache and try again
        * `Failed to communicate with "/interface-data/<libnam>-init?library_id=<libnam>&sort=timestamp.desc&#######", with status: [400 (error)] Bad Request`
* (Optional) Automatically Adding Books to Your calibre Library (This might be utilized through the samba share folder -- Revisit)
  * Create a Calibre Add Book Folder
    * `sudo mkdir -p /path/to/calibre/addbook/folder`
      * The add book folder can be different names if there are multiple calibre servers
  * Change owner
    * `sudo chown <new_user_name>:<new_user_name> /path/to/calibre/addbook/folder`
  * Provide permission to the calibre user
    * `sudo chmod ugo+w /path/to/calibre/addbook/folder`
  * Run the following command to download this book to your server
    * `wget https://www.gutenberg.org/ebooks/11.epub.images -o alice.epub`
  * Now open your crontab
    * crontab -e
      * Here we will set up a script to add all files in this directory to calibre and then delete them (adding books to calibre creates a copy of the files in your library directory, so we can remove the originals once they are added.)
      * Add the following content:
        * **IMPORTANT NOTE** username and password may need to be unicode converted as linux does not like some characters
        * `sudo vim /path/to/calibre/library_name`
          * Below minute increment can be adjusted as needed **IMPORTANT NOTE This step does not need to be done as one can be uploaded via the web site**
          * `\*/5 \* \* \* \* calibredb add /path/to/calibre/addbook/folder/ -r --with-library /path/to/calibre/library_name --username mycalibreuser --password mycalibrepassword && rm -r /path/to/calibre/addbook/folder/\*`
          * If having issues with the password not being correct perform the following command instead
          * `\*/5 \* \* \* \* calibredb add /path/to/calibre/addbook/folder/ -r --with-library /path/to/calibre/library_name --username mycalibreuser --password "<f:/path/to/password/file>" && rm -r /path/to/calibre/addbook/folder/\*`
        * Save and close the file.
        * This will run every 5 minutes, so you shouldn’t have to wait long for your new book to show up in the web interface. Wait a few minutes and then reload the library in your local web browser.
* Access the library from an external network
  * Navigate to your router's port forward section
    * Add the port to the IP address
