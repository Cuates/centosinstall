[How To Install VirtualBox On CentOS 8](https://linuxize.com/post/how-to-install-virtualbox-on-centos-8/)<br />
[VirtualBox RPM EL](https://download.virtualbox.org/virtualbox/rpm/el/)<br />
[VirtualBox](https://download.virtualbox.org/virtualbox/)

* Installing VirtualBox on CentOS 8
  * Enable the Oracle’s VirtualBox repository
    * `sudo dnf config-manager --add-repo=https://download.virtualbox.org/virtualbox/rpm/el/virtualbox.repo`
  * At the time of writing this article, the latest stable version of VirtualBox is version 6.1.x. Run the following command to install the VirtualBox-6.1 package
    * Required Extra Packages Before Installing VirtualBox
      * `sudo dnf -y install elfutils-libelf-devel`
    * `sudo dnf -y install VirtualBox-6.1`
      * **WAIT FOR THIS TO FINISH**
  * VirtualBox has been installed on your CentOS 8 system
  * Installing VirtualBox Extension Pack
    * `wget https://download.virtualbox.org/virtualbox/6.1.16/Oracle_VM_VirtualBox_Extension_Pack-6.1.16.vbox-extpack`
      * Once the file is downloaded, import it using the following command
        * `sudo VBoxManage extpack install Oracle_VM_VirtualBox_Extension_Pack-6.1.16.vbox-extpack`
          * You will be presented with the Oracle license and prompted to accept the terms and conditions
            * Type `y` and hit `Enter`
  * Starting VirtualBox
    * You can start it from the command line or
      * Type `VirtualBox`
    * Click on the VirtualBox icon
      * `Activities` -> `Oracle VM VirtualBox`
