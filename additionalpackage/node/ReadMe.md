[How To Install Nodejs On CentOS 8](https://www.digitalocean.com/community/tutorials/how-to-install-node-js-on-centos-8)<br />
[How To Install Nodejs Version 14 On CentOS 8](https://otodiginet.com/software/how-to-install-node-js-version-14-on-centos-8/)<br />
[How To Update Node](https://hosting.review/tutorial/how-to-update-node/)

* Install
  * `sudo dnf install -y nodejs`
  * `sudo rpm -qa | grep nodejs`
* Upgrade
  * `sudo npm install npm@latest -g`
  * `npm --version`
  * `sudo npm install -g n`
     * Exit terminal and re-open a new terminal for changes to take hold
  * `sudo /usr/local/bin/n latest`
  * `/usr/local/bin/node --version`
