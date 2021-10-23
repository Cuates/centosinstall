[Install Use ffmpeg In CentOS 8](https://linuxhint.com/install-use-ffmpeg-in-centos8/)<br />

* Check if you have the EPEL Repository is installed and enabled
  * ` sudo dnf repolist`
* Install Epel Repository if not already installed
  * `sudo dnf install -y epel-release`
* Check again if you have the EPEL Repository is installed and enabled
  * ` sudo dnf repolist`
* Install RPM Fusion Repository
  * `sudo dnf install -y https://download1.rpmfusion.org/free/el/rpmfusion-free-release-8.noarch.rpm`
* Check again if you have the RPM Fusion Repository is installed and enabled
  * ` sudo dnf repolist`
* Enable Power Tools if not already enabled
  * `sudo dnf config-manager --set-enabled powertools`
* Install FFmpeg
  * `sudo dnf install -y ffmpeg ffmpeg-devel`
* Check if FFmpeg was installed successfully
  * `ffmpeg -version`
