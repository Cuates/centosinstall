[Install Latest phpMyAdmin On CentOS 8](https://kifarunix.com/install-latest-phpmyadmin-on-centos-8/)<br />
[PHP MyAdmin](https://www.phpmyadmin.net/)<br />
[PHP MyAdmin Additional Download Files](https://www.phpmyadmin.net/files/)<br />
[PHP MyAdmin Additional Download](https://www.phpmyadmin.net/downloads/)<br />
[Phpmyadmin Blowfish Secret Generator](https://phpsolved.com/phpmyadmin-blowfish-secret-generator/])<br />
[CentOS Repositories](https://centos.pkgs.org/)<br />
[How To Install PhpMyAdmin With Nginx On CentOS 7](https://linuxize.com/post/how-to-install-phpmyadmin-with-nginx-on-centos-7/)<br />
[Error Warning In Libraries Classes Config](https://stackoverflow.com/questions/65641099/phpmyadmin-5-1-0-rc1-5-0-4-error-warning-in-libraries-classes-config-php12)<br />
[How To Install And Secure phpMyAdmin With Nginx](https://www.digitalocean.com/community/tutorials/how-to-install-and-secure-phpmyadmin-with-nginx-on-an-ubuntu-20-04-server)

* Install Required PHP Modules
  * `sudo dnf module -y enable php:remi-8.2`
    * PHP version will vary with the version you installed on you machine
  * `sudo dnf -y install php-{spl,hash,ctype,json,mbstring,zip,gd,curl,xml,common}` OR
  * `sudo dnf -y install php-spl php-hash php-ctype php-json php-mbstring php-zip php-gd php-curl php-xml php-common`
* Download phpMyAdmin
  * **At the time of this writing PHP MyAdmin is `5.1.3`**
  * **Make sure to get the lastes version from the website**
  * `cd ~`
  * `sudo wget https://files.phpmyadmin.net/phpMyAdmin/5.1.3/phpMyAdmin-5.1.3-all-languages.tar.gz`
    * Verify phpMyAdmin with Checksum
      * Download the SHA256 hash for phpMyAdmin-5.1.3-all-languages.tar.gz
        * `sudo wget https://files.phpmyadmin.net/phpMyAdmin/5.1.3/phpMyAdmin-5.1.3-all-languages.tar.gz.sha256`
          * Calculate the SHA256 hash for downloaded file
            * `sha256sum phpMyAdmin-5.1.3-all-languages.tar.gz`
          * Compare the calculated hash with the downloaded hash
            * `cat phpMyAdmin-5.1.3-all-languages.tar.gz.sha256`
      * If all is well, you are good to proceed
* Install phpMyAdmin
  * Since phpMyAdmin comes as a standalone application ready for installation, simply extract it to your Web root directory
    * Extract phpMyAdmin Tarball
      * Create your phpMyAdmin web root directory. You can choose to use a different directory instead of the one created below
        * `sudo mkdir -p /var/www/phpMyAdmin`
          * Next, extract the phpMyAdmin to the directory created above
            * `tar xzf ~/phpMyAdmin-5.1.3-all-languages.tar.gz -C /var/www/phpMyAdmin --strip-components=1`
* Create phpMyAdmin Nginx Server Block
  * `sudo vim /etc/nginx/conf.d/<domain_name>.conf`
    * Paste the following block of code into the file
      * <pre>
        location /phpMyAdmin {
          root /var/www/;
          index index.php index.html index.htm;

          location ~ ^/phpMyAdmin/(.+\.php)$ {
            try_files $uri =404;
            root /var/www/;
            fastcgi_pass php-fpm;
            fastcgi_index index.php;
            fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
            include /etc/nginx/fastcgi_params;
          }

          location ~* ^/phpMyAdmin/(.+\.(jpg|jpeg|gif|css|png|js|ico|html|xml|txt))$ {
            root /var/www/;
          }
        }

        location /phpmyadmin {
          rewrite ^/* /phpMyAdmin last;
        }
        </pre>
      * Save and exit
  * Nginx syntax verification
    * `nginx -t`
  * Restart Nginx and php-fpm
    * `systemctl restart nginx php-fpm`
* Configure phpMyAdmin
  * Copy the sample phpMyAdmin configuration file without the "sample" string in the name
    * `sudo cp /var/www/phpMyAdmin/config.sample.inc.php /var/www/phpMyAdmin/config.inc.php`
      * Create a blowfish secret required for cookie based authentication to encrypt password in cookie. You can generate the blowfish secret online and paste as follows; Else you can create your own blowfish secret.
        * [Blowfish Secret Generator](https://phpsolved.com/phpmyadmin-blowfish-secret-generator/)
          * Copy and paste from generator on website
        * `sudo vim /var/www/phpMyAdmin/config.inc.php`
          * Include a custom blowfish secret or the generated one from the site
            * <pre>
              // $cfg['blowfish_secret'] = ''; /* YOU MUST FILL IN THIS FOR COOKIE AUTH! */
              $cfg['blowfish_secret'] = '<blowfish_secret_code_goes_here>';
              </pre>
      * Enable Template Caching
        * `sudo vim /var/www/phpMyAdmin/config.inc.php`
          * Add the following to end of file
            * <pre>
                /**
                 * Enable template caching
                 */
                $cfg['TempDir'] = '/tmp/phpMyAdmin';
              </pre>
      * Disable Root Login
        * `sudo vim /var/www/phpMyAdmin/config.inc.php`
          * Add the following to the Authentication type if not already present
            * <pre>
                /* Authentication type */
                $cfg['Servers'][$i]['auth_type'] = 'cookie';
                $cfg['Servers'][$i]['AllowNoPassword'] = false;
                $cfg['Servers'][$i]['AllowRoot'] = false;
              </pre>
      * Save and exit
* Allow Nginx to make modifications to the PHP session folder
  * `sudo chgrp -R nginx /var/lib/php/session/`
* Allow Nginx to make modifications to the PHP wsdlcache folder
  * `sudo chgrp -R nginx /var/lib/php/wsdlcache/`
* Allow Nginx to make modifications to the PHP opcache folder
  * `sudo chgrp -R nginx /var/lib/php/opcache/`
* Restart Nginx and PHP-FPM for the changes to take effect
  * `sudo systemctl restart nginx php-fpm`
* Accessing phpMyAdmin
  * `http(s)://your_domain_or_ip_address/phpMyAdmin`
    * Login as database root user if you did not prevent root user from logging into the site. Upon successful authentication, you will land on the phpMyAdmin dashboard
    * You will not be able to login as root user since you block root user from accessing the site
    * Login using another user on the system
