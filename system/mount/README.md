[How To Mount Partition With NTFS File System And Read Write Access](https://linuxconfig.org/How-to-mount-partition-with-ntfs-file-system-and-read-write-access)<br />
[Error Mounting Mount Unknown Filesystem Type NTFS](https://www.linuxquestions.org/questions/linux-newbie-8/error-mounting-mount-unknown-filesystem-type-%27ntfs%27-926355/)<br />
[Mounting Hard Disks Partitions Using Linux Command Line](https://www.makeuseof.com/tag/mounting-hard-disks-partitions-using-linux-command-line/)<br />
[How To Mount And Unmount Storage Devices From The Linux Terminal](https://www.howtogeek.com/414634/how-to-mount-and-unmount-storage-devices-from-the-linux-terminal/)<br />
[How To Mount USB Device In CentOS 7 NTFS And Linux FS](https://systemzone.net/how-to-mount-usb-device-in-centos-7-ntfs-and-linux-fs/)<br />
[Error Mounting Mount Unknown Filesystem Type 'NTFS'](https://forums.centos.org/viewtopic.php?t=1444)<br />
[How To Mount A Windows NTFS Disk In Linux](https://www.rootusers.com/how-to-mount-a-windows-ntfs-disk-in-linux/)<br />
[Mount Unmount USB Drive On Ubuntu Linux](https://fossbytes.com/mount-unmount-usb-drive-on-ubuntu-linux/)<br />
[How To Manage Partitions In CentOS 8 RHEL 8](https://www.osradar.com/how-to-manage-partitions-in-centos-8-rhel-8/)<br />
[Adding A New Disk Drive To A RHEL System](https://www.techotopia.com/index.php/Adding_a_New_Disk_Drive_to_a_RHEL_System)

* NTSF Hard Drives
  * Install Required Packages
    * `sudo dnf -y install epel-release`
  * Linux NTFS User space Driver
    * `sudo dnf -y install ntfs-3g`
  * Check the following path to see if FUSE is installed on the kernel (Your kernel number will vary depending on what version of Linux you have)
      * `ls -lart /lib/modules/4.18.0-193.19.1.el8_2.x86_64/kernel/fs/ | grep fuse`
        * If there is no fuse on the linux kernel system, then proceed with the following commands
          * FUSE module is by default included with CentOS 7 or Red Hat 7 Linux. However, if you find that FUSE module is not present in your kernel, issue the following command to install and load the FUSE driver module.
            * `sudo dnf -y install fuse`
            * `modprobe fuse`
* Checking Your Available Partitions
  * To see your devices and their separate file-systems
    * `lsblk`
* Identifying partition with NTFS file system
  * `fdisk -l | grep NTFS`
* Mount NTFS Hard Disk Drive
  * First create a mount point (directory) for the hard disk
    * `sudo mkdir /mnt/windows01`
    * Mount the NTFS hard disk drive
      * `sudo mount -t ntfs-3g /dev/sdc1 /mnt/windows01/`
        * You may get an error message with mounting
          * <pre>
            NTFS signature is missing.
            Failed to mount '/dev/sdc': Invalid argument
            The device '/dev/sdc' doesn't seem to have a valid NTFS.
            Maybe the wrong device is used? Or the whole disk instead of a
            partition (e.g. /dev/sda, not /dev/sda1)? Or the other way around?
            </pre>
          * If so, then make the necessary changes they recommend
        * You may also get a message when mounting
          * <pre>
            The disk contains an unclean file system (0, 0).
            Metadata kept in Windows cache, refused to mount.
            Falling back to read-only mount because the NTFS partition is in an
            unsafe state. Please resume and shutdown Windows fully (no hibernation
            or fast restarting.)
            </pre>
          * The hard disk has been mounted but is in read only mode
* Mount A Hard Disk Drive
  * First create a mount point (directory) for the hard disk
    * `sudo mkdir /mnt/harddrive01`
  * Mount the NTFS hard disk drive
    * `sudo mount /dev/sdc /mnt/harddrive01/`
* Unmount A Hard Disk Drive
  * Make sure to be a directory above the mount point (directory) or anywhere outside the mount point (directory) to execute the umount command
    * `sudo umount /mnt/windows01/` OR `sudo umount /mnt/harddrive01/`

* Additional Information
  * Optional Using Mount Hard Drive for Samba Share File/Folder
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
