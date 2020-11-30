[CentOS](https://www.centos.org/)<br />
[Error Gpg Check Failed When Upgrading System Using Dnf In Fedora](https://unix.stackexchange.com/questions/410049/error-gpg-check-failed-when-upgrading-system-using-dnf-in-fedora)
* `cat /etc/*-release`
* `cat /etc/redhat-release`
* `sudo dnf makecache`
* `sudo dnf clean all`
* `sudo dnf update`
  * **WAIT FOR THIS TO FINISH**
  * If there are issues with "Error: GPG check FAILED", then execute the following command
    * `sudo dnf update --nogpgcheck`
* `sudo shutdown -r now`
