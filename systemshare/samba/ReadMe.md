[Install Samba On Redhat 8](https://linuxconfig.org/install-samba-on-redhat-8)<br />
[Install Configure Samba CentOS 8](https://www.linuxtechi.com/install-configure-samba-centos-8/)<br />
[How to create a Samba share that is writable from Windows without 777 permissions](https://unix.stackexchange.com/questions/206309/how-to-create-a-samba-share-that-is-writable-from-windows-without-777-permission)<br />
[How to setup Samba for File Sharing in Linux](https://www.youtube.com/watch?v=oRHSrnQueak)<br />
[How to configure samba server in centos 7](https://www.youtube.com/watch?v=IMPEjYoP3N4)<br />
[How To Install And Configure Samba On CentOS 8](https://www.linuxtechi.com/install-configure-samba-centos-8/)<br />
[Guest Access In SMB2 Disabled By Default In Windows](https://docs.microsoft.com/en-us/troubleshoot/windows-server/networking/guest-access-in-smb2-is-disabled-by-default)<br />
[Quick Samba Server Setup On CentOS 7](https://www.youtube.com/watch?v=jGoU3k-b8sc)<br />
[SMB Configuration Manual](https://www.samba.org/samba/docs/current/man-html/smb.conf.5.html)<br />
[Confining Samba with SELinux](https://danwalsh.livejournal.com/14195.html)<br />
[Restorecon](https://linux.die.net/man/8/restorecon)<br />
[10 Linux Restorecon Command Examples To Restore Selinux Context](https://www.techolac.com/linux/10-linux-restorecon-command-examples-to-restore-selinux-context/)<br />
[Sharing A Mounted Drive With Samba On CentOS 7](https://unix.stackexchange.com/questions/391673/sharing-a-mounted-drive-with-samba-on-centos7)<br />
[Add Multiple Groups To Valid Users](https://superuser.com/questions/437495/add-multiple-groups-to-valid-users)<br />
[Samba Share Multi User Access](https://arkit.co.in/samba-share-multi-user-access/)<br />
[Multiple Connections To A Server Or Shared Resource By The Same User Using More](https://stackoverflow.com/questions/24933661/multiple-connections-to-a-server-or-shared-resource-by-the-same-user-using-more)<br />
[Logging Into A Smb File Server Multiple Times With Different Usernames From One Mac](https://derflounder.wordpress.com/2013/05/31/logging-into-a-smb-file-server-multiple-times-with-different-usernames-from-one-mac/)<br />
[smb.conf](https://www.samba.org/samba/docs/current/man-html/smb.conf.5.html)<br />
[Is There Any Way To Prevent A Mac From Creating Dot Underscore Files](https://superuser.com/questions/212896/is-there-any-way-to-prevent-a-mac-from-creating-dot-underscore-files)<br />
[Why Are Dot Underscore Files Created And How Can I Avoid Them](https://apple.stackexchange.com/questions/14980/why-are-dot-underscore-files-created-and-how-can-i-avoid-them)<br />
[110732 Samba Veto Files No Longer Functioning Properly On My Server](https://forums.unraid.net/topic/110732-samba-veto-files-no-longer-functioning-properly-on-my-server/)<br />
[Samba Veto Files Used To Allow Only One Extension To Be Written To The Share](https://linux.samba.narkive.com/gU3xIugh/samba-veto-files-used-to-allow-only-one-extension-to-be-written-to-the-share)

* `sudo dnf -y install samba samba-common samba-client`
* `sudo systemctl enable --now {smb,nmb}`
* `sudo firewall-cmd --get-services`
* `sudo firewall-cmd --info-service samba`
* `sudo firewall-cmd --zone=public --permanent --add-service=samba`
* `sudo firewall-cmd --reload`
* `sudo firewall-cmd --list-services`
* `smbd -V`

### Creating and Sharing Linux File Share
* Delete an Existing Group
  * `sudo groupdel <groupname>`
* Verify Group was Removed
  * `cat /etc/group`
* Remove User from Group
  * `sudo gpasswd -d <username> <groupname>`
* Create a New Group Name for Samba
  * `sudo groupadd <new_group_name>`
* Associate New User Name to New Group Name
  * `sudo useradd <new_user_name> -G <new_group_name>`
* Associate Existing User to Group
  * `sudo usermod -a -G <new_group_name> <existing_user_name>`
* Create New User Name Samba Password
  * `sudo smbpasswd -a <new_user_name>`
    * New SMB password: <new_user_name_samba_password>
* Optional Using Mount Hard Drive
  * If mounted, then umount first before proceeding
    * `sudo umount /path/to/mount/point`
  * Manual Mount
    * `sudo mount /path/to/mount/drive /path/to/mount/point -o context="unconfined_u:object_r:samba_share_t:s0"`
  * Etc Fstab Mount
    * Open /etc/fstab
      * `sudo vim /etc/fstab`
        * Modify or paste the following
          * `UUID=<...> /path/to/mount/point auto defaults,context="unconfined_u:object_r:samba_share_t:s0" 0 0`
      * Save and exit
* After Successful Mount
  * `sudo chmod -R 0777 /path/to/mount/folder`
    * This will help in permission access to all file(s) and folder(s)
* Create a Secured Folder
  * `sudo mkdir -p /path/to/secured/folder`
* Allow to listen through SELinux
  * `sudo chmod -R 0777 /path/to/secured/folder`
  * `sudo chown -R <user_name>:<group_name> /path/to/secured/folder`
  * To survive system relabel
    * `sudo semanage fcontext -a -t samba_share_t '/path/to/secured/folder(/.*)?'`
    * `sudo restorecon -R -v /path/to/secured/folder`
      * **IMPORTANT NOTE Do not add the -F flag to restorecon as it will change the user, role, range portion as well as the type which we do not want**
      * **NOTE: Do not do chcon below, issue when this is executed on other local computers**
        * `sudo chcon -t samba_share_t -R /path/to/secured/folder`
    * Display the SELinux context for particular file and or directory
      * `ls -lZ`
* Make Backup of Existing Conf File
  * `sudo cp -pf /etc/samba/smb.conf /etc/samba/smb.conf.bak`
* Edit and Save /etc/samba/smb.conf **NOTE: Place the following at the end of the file**
  * `sudo vim /etc/samba/smb.conf`
    * <pre>
      [global]
      workgroup = &lt;Windows_Work_Group&gt;
      security = user
      passdb backend = tdbsam
      printing = cups
      printcap name = cups
      load printers = yes
      cups options = raw
      veto files = /._*/.DS_Store/
      
      [&lt;secured_shared_name&gt;]
      comment = Private Share Drive
      path = /path/to/secured/folder
      browsable = yes
      writable = yes
      read only = no
      available = yes
      public = no
      guest ok = no
      create mask = 0777
      directory mask = 0777
      # force user = &lt;new_user_name&gt;
      # force group = @&lt;new_group_name&gt;
      valid users = @&lt;new_group_name&gt;, &lt;new_user_name&gt;
      # read list = &lt;new_user_name&gt;
      # write list = &lt;new_user_name&gt;
      </pre>
* Restart Samba Services
  * `sudo systemctl restart smb.service nmb.service`
* Check Samba settings
  * `sudo testparm`
    * Press Enter for an overview of smb.conf file

### Accessing Linux File Share Via Windows
* Access the Linux file share
  * Windows Key + r
    * `\\Machine_name_or_IP_Address`
    * `\\hosts_windows_alias_name\samba_remote_alias_name`
  * Browse shared folders
    * Login with username and password from above
* Windows 10 error 1219 that does not allow multiple user connections from windows **NOTE: May not be needed**
  * Windows command prompt
    * `net use`
    * `net use /delete *` OR `net use /delete \\Machine_name_or_IP_Address \path\to\secured\folder`
  * Then re-attempt to access the file share
* Windows modification to connect to multiple Samba shares at once
  * Paste and Modify the following at the end of the C:\Windows\System32\drivers\etc\hosts file
    * <pre>
      &lt;IP_Address&gt; &lt;Alias_Name&gt;
      &lt;IP_Address&gt; &lt;Alias_Name&gt;
      &lt;IP_Address&gt; &lt;Alias_Name&gt;
      </pre>
  * Save and Exit
  * Then attempt to map the share again

### Accessing Linux File Share Via Mac
* To connect to an SMB file server using a different username, you can use this procedure
  * In the Finder, choose the Go menu, then select Connect to Server
  * Type the network address for the computer or server in the Server Address field in the following format
    * `smb://username:*@server_name_ip_address`
      * The "*" is to trigger the server login window for your SMB server, so that the password for the other_username account can be entered
    * Click the Connect button
    * Enter the desired username and password when prompted
      * Username: other_username
      * Password: The current account password for other_username
      * Select the share on your SMB server that you want to use
      * ** WARNING: Do not try to mount the same share twice using different usernames **
  * One way you can verify that you’re actually connected using different usernames is to use the mount command in Terminal. This should show all mounted volumes on the Mac, including mounted fileshares. The fileshare mount information should include which account was used to mount the share
    * Open a terminal
      * `mount`
  * ** NOTE: Depending on your file server, this approach may not work consistently. On our Isilon storage, the SMB share would mount with the user-specified username every time. On another server I tested, the server would prefer the specific username that was last used to connect and keep using that username when mounting additional shares **
