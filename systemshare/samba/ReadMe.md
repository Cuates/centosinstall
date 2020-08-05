[Install Samba On Redhat 8](https://linuxconfig.org/install-samba-on-redhat-8)<br />
[Install Configure Samba CentOS 8](https://www.linuxtechi.com/install-configure-samba-centos-8/)
* `sudo dnf install samba samba-common samba-client`
* `sudo systemctl enable --now {smb,nmb}`
* `sudo firewall-cmd --info-service samba`
* `sudo firewall-cmd --permanent --add-service=samba`
* `sudo firewall-cmd --reload`
* `sudo firewall-cmd --list-services`
* `smbd -V`
