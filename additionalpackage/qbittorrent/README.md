[Install Qbittorrent Centos 8 RHEL 8](https://www.linuxbabe.com/redhat/install-qbittorrent-centos-8-rhel-8)<br />
[How To Instal Qbittorrent On Desktop Server Centos 8 RHEL 8](https://tier4hosting.com/how-to-instal-qbittorrent-on-desktop-server-centos-8-rhel-8/)

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
* The qbittorrent-nox package ships with the needed systemd service file
  * Under /usr/lib/systemd/system/ directory you will find qbittorrent-nox@.service
    * Make a copy of the file /usr/lib/systemd/system/qbittorrent-nox@.service to /etc/systemd/system/qbittorrent-nox@<username>.service
    * Replace username with your actual username
      * `sudo cp /usr/lib/systemd/system/qbittorrent-nox@.service /etc/systemd/system/qbittorrent-nox@<username>.service`
      * Enable qbittorrent-nox to auto-start at boot time by running the below command
        * `sudo systemctl enable qbittorrent-nox@<username>.service`
      * Now we can start the qBittorrent service with the following command
        * `sudo systemctl start qbittorrent-nox@<username>.service`
      * Check status
        * `sudo systemctl status qbittorrent-nox@<username>.service`
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
