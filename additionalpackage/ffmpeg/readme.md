[Install Use ffmpeg In CentOS 8](https://linuxhint.com/install-use-ffmpeg-in-centos8/)<br />

NOTE: Version 9 does not have powertools
* You can skip the powertools installation steps
* Go straight to install FFmpeg package

* Check if you have the EPEL Repository is installed and enabled
  * ` sudo dnf repolist`
* Install Epel Repository if not already installed
  * `sudo dnf install -y epel-release`
* Check again if you have the EPEL Repository is installed and enabled
  * ` sudo dnf repolist`
* Install RPM Fusion Repository
  * One of the below version will be utilized. Make sure to install the correct one for the version of your linux system.
    * Version 8
      * `sudo dnf install -y https://download1.rpmfusion.org/free/el/rpmfusion-free-release-8.noarch.rpm`
    * Version 9
      * `sudo dnf install -y https://download1.rpmfusion.org/free/el/rpmfusion-free-release-9.noarch.rpm`
* Check again if you have the RPM Fusion Repository is installed and enabled
  * ` sudo dnf repolist`
* Enable Power Tools if not already enabled
  * `sudo dnf config-manager --set-enabled powertools`
* Install FFmpeg
  * `sudo dnf install -y ffmpeg ffmpeg-devel`
* Check if FFmpeg was installed successfully
  * `ffmpeg -version`
