[2 ways to install unrar on rocky linux almalinux 8](https://www.how2shout.com/linux/2-wyas-to-install-unrar-on-rocky-linux-almalinux-8/)<br />
[Rar UnRar](https://centos.pkgs.org/8/forensics-x86_64/rar-5.4.0-1.el8.x86_64.rpm.html)<br />
[Forensics](https://forensics.cert.org/)

* `sudo dnf install -y https://forensics.cert.org/cert-forensics-tools-release-el8.rpm`
  * **NOTE** https://forensics.cert.org/ is no longer maintained
    * Look for an alternative or stop using this repository
* `sudo dnf update cert-forensics-tools-release`
* `sudo dnf --enablerepo=forensics install -y rar`
* `sudo dnf --enablerepo=forensics install -y unrar`

`https://download1.rpmfusion.org/nonfree/el/rpmfusion-nonfree-release-9.noarch.rpm`
