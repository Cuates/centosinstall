[How To Install Xrdp On Centos 8](https://linuxize.com/post/how-to-install-xrdp-on-centos-8/)<br />
[centos-desktop-rdp-xrdp](https://vitux.com/centos-desktop-rdp-xrdp/)<br />
[How To Install Xrdp Remote Desktop On Centos 8 How To Use Windows To Remote Control Centos 8](https://dannyda.com/2020/02/09/how-to-install-xrdp-remote-desktop-on-centos-8-how-to-use-windows-to-remote-control-centos-8/)<br />
[How To Install Xrdp Server Remote Desktop On Centos 8](https://www.mstvlife.com/how-to-install-xrdp-server-remote-desktop-on-centos-8/)

* Installing Desktop Environment (Optional)
  * Generally, Linux servers don’t have a desktop environment installed. If the machine you want to connect to doesn’t have GUI, the first step is to install it. Otherwise, skip this step.
  * Install Gnome on your remote machine
    * `sudo dnf -y groupinstall "Server with GUI"`
* Installing Xrdp
  * EPEL Software repository
    * `sudo dnf -y install epel-release`
  * Install Xrdp package
    * `sudo dnf -y install xrdp`
  * Check version
    * `xrdp --version`
  * Start the Xrdp service and enable it at boot
    * `sudo systemctl enable xrdp --now`
  * If you want to execute enable and start separately perform the following
    * Enable at boot
      * `sudo systemctl enable xrdp`
    * Start Xrdp
      * `sudo systemctl start xrdp`
  * Verify that Xrdp is running
    * `sudo systemctl status xrdp`
* Configuring Xrdp
  * The configuration files are located in the /etc/xrdp directory
  * The main configuration file is named xrdp.ini. This file is divided into sections and allows you to set global configuration settings such as security and listening addresses and create different xrdp login sessions.
  * Modify xrdp.ini file
    * `sudo vim /etc/xrdp/xrdp.ini`
    * Add the following line at the end of the file
      * `exec gnome-session`
    * Save and Exit
  * Restart whenever changes are made to xrdp.ini
    * `sudo systemctl restart xrdp`
      * Xrdp uses startwm.sh file to launch the X session. If you want to use another X Window desktop, edit this file.
* Configure Firewall
  * By default, Xrdp listens on port 3389 on all interfaces
  * Typically you would want to allow access to the Xrdp server only from a specific IP address or IP range. For example, to allow connections only from the 192.168.1.0/24 range, enter the following command
    * `sudo firewall-cmd --get-services`
    * `sudo firewall-cmd --new-zone=xrdp --permanent`
    * `sudo firewall-cmd --zone=xrdp --add-port=3389/tcp --permanent`
    * `sudo firewall-cmd --zone=xrdp --add-source=192.168.1.0/24 --permanent`
    * `sudo firewall-cmd --reload`
    * `sudo firewall-cmd --list-ports`
    * `sudo firewall-cmd --list-all`
  * To allow traffic to port 3389 from anywhere use the commands below. Allowing access from anywhere is highly discouraged for security reasons.
    * `sudo firewall-cmd --get-services`
    * `sudo firewall-cmd --zone=public --permanent --add-port=3389/tcp`
    * `sudo firewall-cmd --reload`
    * `sudo firewall-cmd --list-ports`
    * `sudo firewall-cmd --list-all`
  * **IMPORTANT NOTE For increased security, you may consider setting up Xrdp to listen only on localhost and creating an SSH tunnel that securely forwards traffic from your local machine on port 3389 to the server on the same port. Another secure option is to install OpenVPN and connect to the Xrdp server through the private network.**
* Connecting to the Xrdp Server
  * You can now start interacting with the remote desktop from your local machine using your keyboard and mouse.
  * If you are using macOS, you can install the Microsoft Remote Desktop application from the Mac App Store. Linux users can use an RDP client such as Remmina or Vinagre. Windows can use the Remote Desktop Connection (RDP) which is already installed on Windows.
  * Launch your remote desktop of choice
  * Put in the IP address of the Linux server
  * Input username and password
  * You may get a message for "Authenticate Required to access the PC/SC daemon"
    * Input password for the user currently trying to remote into the system
    * Click Authenticate
