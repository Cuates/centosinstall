[Install Ruby On Rails CentOS 8](https://www.osradar.com/install-ruby-on-rails-centos-8/)

* **IMPORTANT NOTE**
  * Login into the root user first
  *   * [Ruby Dependent](https://github.com/Cuates/centosinstall/tree/master/additionallanguage/ruby)
* `source /etc/profile.d/rvm.sh`
* `gem install rails` (side note to install a specific version: `gem install rails -v 6.1.3.1`)
  * **WAIT FOR THIS TO FINISH**
  * If presented with the following messages
    * Install package 'rubygems' to provide command 'gem'? y
    * Proceed with changes? y
* `rails -v`
