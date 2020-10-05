[Install Samba On Redhat 8](https://linuxconfig.org/install-samba-on-redhat-8)<br />
[Install Configure Samba CentOS 8](https://www.linuxtechi.com/install-configure-samba-centos-8/)<br />
[How to create a Samba share that is writable from Windows without 777 permissions](https://unix.stackexchange.com/questions/206309/how-to-create-a-samba-share-that-is-writable-from-windows-without-777-permission)<br />
[How to setup Samba for File Sharing in Linux](https://www.youtube.com/watch?v=oRHSrnQueak)<br />
[How to configure samba server in centos 7](https://www.youtube.com/watch?v=IMPEjYoP3N4)<br />
[How To Install And Configure Samba On CentOS 8](https://www.linuxtechi.com/install-configure-samba-centos-8/)<br />
[Guest access in SMB2 disabled by default in Windows](https://docs.microsoft.com/en-us/troubleshoot/windows-server/networking/guest-access-in-smb2-is-disabled-by-default)<br />
[Quick Samba Server Setup on CentOS 7](https://www.youtube.com/watch?v=jGoU3k-b8sc)

* `sudo dnf -y install samba samba-common samba-client`
* `sudo systemctl enable --now {smb,nmb}`
* `sudo firewall-cmd --get-services`
* `sudo firewall-cmd --info-service samba`
* `sudo firewall-cmd --zone=public --permanent --add-service=samba`
* `sudo firewall-cmd --reload`
* `sudo firewall-cmd --list-services`
* `smbd -V`

### Creating and Sharing Linux File Share
* Create a New Group Name for Samba
  * `sudo groupadd <new_group_name>`
* Associate New User Name to New Group Name
  * `sudo useradd <new_user_name> -G <new_group_name>`
* Associate Existing User to Group
  * `sudo usermod -a -G <new_group_name> <existing_user_name>`
* Create New User Name Samba Password
  * `sudo smbpasswd -a <new_user_name>`
    * New SMB password: <new_user_name_samba_password>
* Create a Secured Folder
  * `sudo mkdir -p /path/to/secured/folder`
* Allow to listen through SELinux
  * `sudo chmod -R 0777 /path/to/secured/folder`
  * `sudo chown -R <user_name>:<user_name> /path/to/secured/folder`
  * `sudo chcon -t samba_share_t -R /path/to/secured/folder`
    * To survive system relabel
      * `sudo semanage fcontext -a -t samba_share_t '/path/to/secured/folder(/.*)'`
      * `sudo restorecon -vRF /path/to/secured/folder` **NOTE: Do not do chcon above, issue when this is executed on other local computers, does not give what we want**
* Make Backup of Existing Conf File
  * `sudo cp -pf /etc/samba/smb.conf /etc/samba/smb.conf.bak`
* Edit and Save /etc/samba/smb.conf **NOTE: Place the following at the end of the file**
  * `sudo vim /etc/samba/smb.conf`
    * [global]<br />
      workgroup = <Windows_Work_Group><br />
      security = user<br />
      passdb backend = tdbsam<br />
      printing = cups<br />
      printcap name = cups<br />
      load printers = yes<br />
      cups options = raw
    * [<secured_shared_name>]<br />
      comment = Private Share Drive<br />
      path = /path/to/secured/folder<br />
      browsable = yes<br />
      writable = yes<br />
      read only = no<br />
      available = yes<br />
      public = yes<br />
      create mask = 0777<br />
      directory mask = 0777<br />
      force user = <new_user_name><br />
      \# force group = @<new_group_name><br />
      \# valid users = <new_user_name><br />
      \# valid group = @<new_group_name><br />
      \# read list = <new_user_name><br />
      \# write list = <new_user_name>
* Restart Samba Services
  * `sudo systemctl restart smb.service nmb.service`
* Check Samba settings
  * `sudo testparm`
    * Press Enter for an overview of smb.conf file

### Accessing Linux File Share Via Windows
* Access the Linux file share
  * Windows Key + r
    * `\\Machine_name_or_IP_Address`
  * Browse shared folders
    * Login with username and password from above
* Windows 10 error 1219 that does not allow multiple user connections from windows **NOTE: May not be needed**
  * Windows command prompt
    * `net use`
    * `net use /delete *` OR `net use /delete \\Machine_name_or_IP_Address \path\to\secured\folder`
  * Then re-attempt to access the file share
