[How To Mount cifs Windows Share On Linux](https://linuxize.com/post/how-to-mount-cifs-windows-share-on-linux/) <br />

Make sure to have cifs-utils installed before proceeding with these steps

# Create directory to mount the shared drive in
* `cd /mnt`
* `mkdir <share_directory_name>`

# Credital file for the shared drive
* Create credential file
  * `cd /etc`
  * `vim <credential_file_name>`
    * <pre>
        username=username
        password=password
      </pre>
* Set file permissions for root user only
  * `sudo chown root: /etc/<credential_file_name>`
  * `sudo chmod 600 /etc/<credential_file_name>`

# Configure fstab
  * `vim /etc/fstab`
    * <pre>
        # <file system>             <dir>          <type> <options>                                                   <dump>  <pass>
        //WIN_SHARE_IP/share_name  /mnt/<share_directory_name>  cifs  credentials=/etc/<credential_file_name>,file_mode=0777,dir_mode=0777 0 0
      </pre>
