[Rar UnRar](https://centos.pkgs.org/8/forensics-x86_64/rar-5.4.0-1.el8.x86_64.rpm.html)<br />
[Forensics](https://forensics.cert.org/)

* `sudo dnf install -y https://dl.fedoraproject.org/pub/epel/epel-release-latest-9.noarch.rpm`
* **NOTE** https://forensics.cert.org/ is no longer maintained
  * Look for an alternative or stop using this repository
* `sudo dnf update cert-forensics-tools-release`
* `sudo dnf --enablerepo=forensics install -y rar`
* `sudo dnf --enablerepo=forensics install -y unrar`
