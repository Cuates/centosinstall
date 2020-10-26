[Install VMWare Workstation Pro 15 CentOS 8](https://linuxhint.com/install_vmware_workstation_pro_15_centos8/)<br />
[Install VMWare Workstation On CentOS](https://computingforgeeks.com/install-vmware-workstation-on-centos/)<br />
[workstation Pro](https://www.vmware.com/products/workstation-pro.html)<br />
[Workstation Pro Evaluation](https://www.vmware.com/products/workstation-pro/workstation-pro-evaluation.html)

* Installing Required Dependencies
  * `sudo dnf -y groupinstall "Development Tools"`
  * You also need to have elfutils-libelf-devel package installed for VMware Kernel Module building to work
    * `sudo dnf -y install elfutils-libelf-devel`
* Downloading VMware Workstation Pro 16
  * At the time of writing this article, the latest stable version of VMWare Workstation is version 16.x.
    * Command Line or
      * `wget https://download3.vmware.com/software/wkst/file/VMware-Workstation-Full-16.0.0-16894299.x86_64.bundle`
        * **WAIT FOR THIS TO FINISH**
    * Through Web Browser
      * First, visit the official website (https://www.vmware.com/products/workstation-pro.html) of VMware Workstation Pro. Once the page loads, click on Download Now >> (https://www.vmware.com/products/workstation-pro/workstation-pro-evaluation.html)
        * Click on Download Now >> in the Workstation 16 Pro for Linux section (https://download3.vmware.com/software/wkst/file/VMware-Workstation-Full-16.0.0-16894299.x86_64.bundle)
* Installing VMware Workstation Pro
  * Add executable permission to the VMware Workstation Pro 16 installer binary
    * `sudo chmod +x VMware-Workstation-Full-16.0.0-16894299.x86_64.bundle`
      * Run the VMware Workstation Pro 16 installer binary
        * `sudo ./VMware-Workstation-Full-16.0.0-16894299.x86_64.bundle`
          * **WAIT FOR THIS TO FINISH**
  * VMware Workstation Pro 16 has been installed on your CentOS 8 system
    * Navigate to the Linux GUI to proceed with the rest of the process
      * Click on the VMware Workstation icon
        * `Activities` -> `VMware Workstation`
          * VMware Kernel Module installer may show up (optional)
            * Click on `Install`
              * Type in the `password` of your login user and click on Authenticate
                * **WAIT FOR THIS TO FINISH**
          * Select `I accept the terms in the license agreement`
            * Click on `Next` to accept the VMware Workstation License Agreement
          * Select `I accept the terms in the license agreement`
            * Click on `Next` to accept the VMware OVF Tool License Agreement
          * If you want VMware Workstation to check for updates when you start VMware Workstation Pro, then select Yes. Otherwise, select `No`. Then, click on `Next`.
          * If you want to join VMware Customer Experience Improvement Program (CEIP), then select Yes. Otherwise, select `No`. Then, click on `Next`.
          * License Key
            * Enter your `license key` if you have one else skip and use `trial version` instead
            * Click `Finish`
          * VMware Workstation Pro 16 should start. Click on `OK`.
