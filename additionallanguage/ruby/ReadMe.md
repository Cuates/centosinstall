[install ruby on rails on rocky almalinux 9](https://computingforgeeks.com/install-ruby-on-rails-on-rocky-almalinux/)<br />
[Install Ruby CentOS 8](https://www.osradar.com/install-ruby-centos-8/)
* **IMPORTANT NOTE**
  * Login into the root user first
* `sudo dnf install -y curl gnupg2 tar`
* `sudo curl -sSL https://get.rvm.io | bash`
* `source /etc/profile.d/rvm.sh`
* `usermod -a -G rvm <username_on_system>`
  * **IMPORTANT NOTE**
    * Exit out of the terminal
    * Logout and log back into the system
    * Reopen a new terminal
* `source /etc/profile.d/rvm.sh`
* `rvm requirements`
* `rvm list known`
* `rvm install 3.1.3` **Pick the latest MRI Rubies version**
  * **WAIT FOR THIS TO FINISH**
  * If built without documentation message is presented (OPTIONAL STEP)
    * `rvm docs generate-ri`
      * **WAIT FOR THIS TO FINISH**
* `rvm use 3.1.3 --default`
  * As of this time 3.2.0+ is not ready for AlmaLinux
* `ruby --version`
* Remove rvm
  * `rvm implode`
    * Are you SURE you wish for rvm to implode? yes
    * If the files still exist, manually remove
      * `/etc/rvmrc`
      * `~/.rvmrc`
