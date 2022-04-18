[NVM](https://github.com/nvm-sh/nvm) <br />
[How To Install Node JS On CentOS 8](https://www.digitalocean.com/community/tutorials/how-to-install-node-js-on-centos-8)

* If installing [NodeJS](https://github.com/Cuates/centosinstall/blob/master/additionalpackage/node) does not work through the command line, then use the NVM to install NodeJS
* Installing Node Version Manager (NVM)
  * Go to the github repository to get the latest version
    * Execute the following line with the version you download from github
      * `curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash`
  * Close and reopen terminal or source your profile
    * This will install the nvm script to your user account.
    * To use it, you must first source your .bash_profile file
  * You can see the different versions you have installed by typing
    * `nvm list`
  * Install Nodejs version of choice
    * Install the latest version using one of the following commands below. NOTE: Your Nodejs version might be different with what is shown below.
      * `nvm install v16.14.0`
      * `nvm install lts/gallium`
  * You can verify that the install was successful using the same technique from the other sections, by typing:
    * `node --version`
* Uninstalling Node Version Manager (NVM)
  * If you wish to uninstall them at a later point (or re-install them under your 'nvm' Nodes), you can remove them from the system Node as follows:
    * Execute the following command to remove nvm from your system
      * `nvm use system`
      * `npm uninstall -g a_module`
