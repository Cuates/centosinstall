[Install Ruby CentOS 8](https://www.osradar.com/install-ruby-centos-8/)
* **IMPORTANT NOTE**
  * Login into the root user first
* `sudo dnf install -y curl gnupg2 tar`
* `sudo curl -sSL https://get.rvm.io | bash`
* `source /etc/profile.d/rvm.sh`
* `usermod -a -G rvm <username_on_system>`
  * **IMPORTANT NOTE**
    * Exit out of the terminal and reopen a new terminal
* `source /etc/profile.d/rvm.sh`
* `rvm requirements`
* `rvm list known`
* `rvm install 3.0.1` **Pick the latest MRI Rubies version**
  * **WAIT FOR THIS TO FINISH**
* `rvm use 3.0.1 --default`
* `ruby --version`
