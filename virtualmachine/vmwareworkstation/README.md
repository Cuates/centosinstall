[Install VMWare Workstation Pro 15 CentOS 8](https://linuxhint.com/install_vmware_workstation_pro_15_centos8/)<br />
[Install VMWare Workstation On CentOS](https://computingforgeeks.com/install-vmware-workstation-on-centos/)<br />
[workstation Pro](https://www.vmware.com/products/workstation-pro.html)<br />
[Workstation Pro Evaluation](https://www.vmware.com/products/workstation-pro/workstation-pro-evaluation.html)<br />
[VMWare vmrun Command](https://www.vmware.com/pdf/vix160_vmrun_command.pdf)<br />
[Syntax Of vmrun Commands](https://docs.vmware.com/en/VMware-Fusion/12/com.vmware.fusion.using.doc/GUID-24F54E24-EFB0-4E94-8A07-2AD791F0E497.html)
[vmware Command Options](https://docs.vmware.com/en/VMware-Workstation-Pro/16.0/com.vmware.ws.using.doc/GUID-7369457F-FE1D-40FE-97B6-B29CA4916CCD.html#GUID-7369457F-FE1D-40FE-97B6-B29CA4916CCD)<br />
[Run The vmware Command](https://docs.vmware.com/en/VMware-Workstation-Pro/16.0/com.vmware.ws.using.doc/GUID-DA203314-F153-4F1F-8FCF-A7700530943D.html)

* Installing Required Dependencies
  * `sudo dnf -y groupinstall "Development Tools"`
  * You also need to have elfutils-libelf-devel package installed for VMware Kernel Module building to work
    * `sudo dnf -y install elfutils-libelf-devel`
* Downloading VMware Workstation Pro 16
  * At the time of writing this article, the latest stable version of VMWare Workstation is version 16.x.
    * Command Line or
      * `wget https://download3.vmware.com/software/wkst/file/VMware-Workstation-Full-16.2.3-19376536.x86_64.bundle`
        * **WAIT FOR THIS TO FINISH**
    * Through Web Browser
      * First, visit the official website (https://www.vmware.com/products/workstation-pro.html) of VMware Workstation Pro. Once the page loads, click on Download Now >> (https://www.vmware.com/products/workstation-pro/workstation-pro-evaluation.html)
        * Click on Download Now >> in the Workstation 16 Pro for Linux section (https://download3.vmware.com/software/wkst/file/VMware-Workstation-Full-16.2.3-19376536.x86_64.bundle)
* Installing VMware Workstation Pro
  * Add executable permission to the VMware Workstation Pro 16 installer binary
    * `sudo chmod +x VMware-Workstation-Full-16.2.3-19376536.x86_64.bundle`
      * Run the VMware Workstation Pro 16 installer binary
        * `sudo ./VMware-Workstation-Full-16.2.3-19376536.x86_64.bundle`
          * **WAIT FOR THIS TO FINISH**
          * VMWare Workstation
            * If the installation complains about System service scripts directory (commonly /etc/init.d), the create a folder called init.d inside the /etc direct
              * Must be root user to perform the following task
                * `mkdir /etc/init.d`
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

* Additional Commands
  * Start Stop VMWare Workstation Via Command Line
    * Start
      * `sudo /usr/bin/vmrun -T ws start /path/to/virtual/machine/file.vmx nogui`
    * Stop
      * `sudo /usr/bin/vmrun -T ws stop /path/to/virtual/machine/file.vmx soft`

* VMWare Uninstall Command Line
  * vmware-installer -l
    * Note Product Name
  * vmware-installer -u <Product Name>
    * Do you wish to keep your configuration files?
      * Type: No
