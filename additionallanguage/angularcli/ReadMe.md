[Install Angular CentOS 8](https://idroot.us/install-angular-centos-8/)
[Install Angular Cli On CentOS](https://tecadmin.net/install-angular-cli-on-centos/)
* `sudo dnf clean all`
* `sudo dnf update`
* `sudo dnf module -y install nodejs`
  * **NOTE Perform the above only if not installed already**
* `sudo npm install -g npm@latest`
  * **NOTE Perform the above only if not installed already**
* `sudo dnf module -y install nodejs/development`
* `node -v`
* `sudo npm install -g @angular/cli`
  * **WAIT FOR THIS TO FINISH**
  * Share anonymous usage data: N
* Check global versions of the web application
  * Execute either of the commands to see the version numbers installed
    * `sudo npm list -global --depth 0`
    * `ng --version`
* Uninstall Angular from command line
  * `sudo npm uninstall -g @angular/cli`
