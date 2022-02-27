[How To Install Nodejs On CentOS 8](https://www.digitalocean.com/community/tutorials/how-to-install-node-js-on-centos-8)<br />
[How To Install Nodejs Version 14 On CentOS 8](https://otodiginet.com/software/how-to-install-node-js-version-14-on-centos-8/)<br />
[How To Update Node](https://hosting.review/tutorial/how-to-update-node/)<br />
[NPM N Module](https://www.npmjs.com/package/n)

* Install
  * `sudo dnf install -y nodejs`
  * `sudo rpm -qa | grep nodejs`
* Upgrade
  * `sudo npm install npm@latest -g`
  * `sudo npm cache clean -f`
  * `sudo npm install -g n`
     * Exit terminal and re-open a new terminal for changes to take hold
  * `sudo /usr/local/bin/n latest` OR `sudo n latest`
  * `/usr/local/bin/node --version` OR `node --version`
  * `npm --version`
* Remove Existing NodeJS Module
  * `sudo dnf remove -y nodejs`
* List Available NodeJS Modules
  * `sudo dnf module list | grep nodejs` OR `sudo dnf module list nodejs`
* Reset NodeJS Module
  * `suod dnf module reset nodejs`
* Enable NodeJS Module Version
  * `sudo dnf module -y enable nodejs:<stream>`
  * * i.e. `sudo dnf module -y enable nodejs:16`
* Install Specific NodeJS Module
  * `sudo dnf module install -y nodejs:<stream>`
    * i.e. `sudo dnf module install -y nodejs:16`
