[Install Nginx CentOS 8](https://phoenixnap.com/kb/install-nginx-centos-8)<br />
[Redirect HTTP To HTTPS Nginx](https://phoenixnap.com/kb/redirect-http-to-https-nginx)<br />
[Nginx Reverse Proxy](https://phoenixnap.com/kb/nginx-reverse-proxy)<br />
[How To Set Up Nginx Server Blocks Virtual Hosts CentOS 7](https://phoenixnap.com/kb/how-to-set-up-nginx-server-blocks-virtual-hosts-centos-7)<br />
[How To Install Nginx Webserver On CentOS 8](https://www.linuxgurus.in/how-to-install-nginx-webserver-on-centos-8/)<br />
[How To Install Nginx On CentOS 8](https://www.digitalocean.com/community/tutorials/how-to-install-nginx-on-centos-8)<br />
[How To Install And Use Nginx On CentOS 8](https://www.cyberciti.biz/faq/how-to-install-and-use-nginx-on-centos-8/)<br />
[Install PHP 7 X On CentOS 8 For Nginx](https://www.cyberciti.biz/faq/install-php-7-x-on-centos-8-for-nginx/)<br />
[Server Blocks](https://www.nginx.com/resources/wiki/start/topics/examples/server_blocks/)<br />
[How To Set Up Nginx Server Blocks Virtual Hosts On Ubuntu 16.04](https://www.digitalocean.com/community/tutorials/how-to-set-up-nginx-server-blocks-virtual-hosts-on-ubuntu-16-04)<br />
[CentOS 8 And Nginx](https://www.server-world.info/en/note?os=CentOS_8&p=nginx&f=1)

*  Installation of EPEL (Extra Package for Enterprise Linux) repository
  * `sudo dnf -y install epel-release`
* View the available Nginx versions
  * `dnf module list nginx`
* Enabling the latest Nginx web server module
  * `sudo dnf module enable nginx:1.16`
    * Your version may differ depending on what version shows in the module
    * Type y and click Enter key to complete the modifications
  * If error message is given "Error: It is not possible to switch enabled streams of a module"
    * Command to reset the module for Nginx
      * `sudo dnf module reset nginx`
        * Type y and click Enter
    * Run the enable command above again
* Optional Commands
  * List Nginx packages
    * `sudo dnf list nginx`
  * Search for Nginx packages
    * `sudo dnf search nginx`
  * Inspect the Nginx package before adding it to your system
    * Request to see the RPM metadata included in every RPM package
      * `sudo dnf info nginx`
* Install Nginx
  * `sudo dnf -y install nginx`
* Start the service
  * `sudo systemctl start nginx`
* To enable the service to start running upon boot time use
  * `sudo systemctl enable nginx`
* If you check the service status, the output should show you Nginx is active (running)
  * `sudo systemctl status nginx`
* Additional Commands
  * Start service and Enable service at boot up
    * `sudo systemctl enable --now nginx`
  * Stop Nginx Service
    * `sudo systemctl stop nginx`
  * Restart Nginx Service
    * `sudo systemctl restart nginx`
  * Reload the configuration files without stopping the service
    * `sudo systemctl reload nginx`
  * To check if it is enabled on startup
    * `sudo systemctl is-enabled nginx`
  * Disable the Nginx service from startup
    * `sudo systemctl disable nginx`
  * To test Nginx
    * `sudo service nginx configtest`
    * `sudo nginx -t`
* Open Firewall port and or services
  * Open port HTTP and HTTPS
    * `sudo firewall-cmd --permanent --zone=public --add-service=http --add-service=https`
  * Reload Firewall settings
    * `sudo firewall-cmd --reload`
  * List services from the firewall
    * `sudo firewall-cmd --list-services --zone=public`
* Use Netstat to list all open ports and verify whether you have successfully opened 80 and 443
  * `netstat -tulpn`
  * Alternative to verifing that TCP port 80 or 443 opened
    * `sudo ss -tulpn`
* Double-check Nginx is working by visiting your public IP address (or domain name)
  * To see the IP address of your server, type the following command in the terminal
    * `ip addr`
    * Alternative
      * `ip a`
  * Find the IP address and copy it
  * Open a web browser and paste the IP address (or domain name) in the URL bar. This should open the Nginx Welcome Page, confirming you have successfully installed and set up the server
  * One can also use the curl command to get same info using the cli
    * `curl -I http://<ip_address>`
    * `curl http://<ip_address>`
* Configure the domain_name.conf file
  * Create a new domain_name.con file at the following location
    * `/etc/nginx/conf.d/domain_name.conf`
      * Paste the following in the domain_name.conf file
       * <pre>
         server {
           listen 80;
           listen [::]:80;

           root /var/www/html;
           index index.html index.htm index.php;

           server_name cuateslws.ddns.net;

           location / {
           # By default, Nginx buffers traffic for servers that it proxies for. Buffers improve server performance as a server response isn’t sent until the client finishes sending a complete response. To turn the buffer off.
           # proxy_buffering off;
           try_files $uri $uri/ =404;
           }

           # Setting up php within Nginx
           location ~ \.php$ {
           try_files $uri =404;
           fastcgi_intercept_errors on;
           fastcgi_index  index.php;
           include        fastcgi_params;
           fastcgi_param  SCRIPT_FILENAME  $document_root$fastcgi_script_name;
           fastcgi_pass   php-fpm;
           }
         }
         </pre>
     * Test Nginx
          * `sudo nginx -t`
     * Restart Nginx Service
       * `sudo systemctl restart nginx`
* Optional you don’t need to configure Nginx upon installation. However, you should know the location of the configuration files and the Nginx root directory in case you need to modify the configuration.
  * Nginx configuration directory: `/etc/nginx`
  * Nginx root directory: `/usr/share/nginx/html`
  * Master/Global configuration file: `/etc/nginx/nginx.conf`
    * `/etc/nginx/conf.d/`: This directory contains server block configuration files, where you can define the websites that are hosted within Nginx. A typical approach is to have each website in a separate file that is named after the website’s domain name, such as your_domain.conf.
  * Server Logs
    * `/var/log/nginx/access.log`
      * All the requests come to your server are listed in access.log. But, you can change this location in the configuration file.
    * `/var/log/nginx/error.log`
      * All the errors are recorded in the error.log file
  * This is the default location to store the Nginx welcome page. This is located at in directory `/usr/share/nginx/html`. You can change it after modifying the Nginx configuration file
  * If you wanted to change the Global configuration file, you would open it (etc/nginx/nginx.conf) with a text editor and apply the changes.
    * One common use case is editing the Nginx configuration file to redirect HTTP traffic to HTTPS
  * Create New Configuration File (optional steps)
    * Sites-available directory to store the server blocks in
      * `sudo mkdir /etc/nginx/sites-available`
    * Sites-enabled directory that will tell Nginx which links to publish and which blocks share content with visitors
      * `sudo mkdir /etc/nginx/sites-enabled`
    * Then, open the Nginx configuration file and modify it by adding the sites-enabled directory
      * `sudo vim /etc/nginx/nginx.conf`
      * This will be done within the server block of code from below
        * Inside the http block, add the following two lines
          * <pre>
            include /etc/nginx/sites-enabled/*.conf
            server_names_hash_bucket_size 64;
            </pre>
          * Save and exit
        * Enable Server Block Files
          * To enable the virtual host files, create symbolic links in the sites-enabled directories with the commands
            * `sudo ln -s /etc/nginx/sites-available/your_domain.conf /etc/nginx/sites-enabled/your_domain.conf`
        * Test Nginx
          * `sudo nginx -t`
        * Restart Nginx Service
          * `sudo systemctl restart nginx`
  * Setting Up Server Blocks
    * You have to set up server blocks. It works similar to the Apache virtual host. You can set the server to respond to multiple domain names and provide different content for each of them.
      * Server blocks are defined by .conf file which is located in `/etc/nginx/conf.d`.
    * Creating a server block
      * Create the directory for your_domain as follows, using the -p flag to create any necessary parent directories:
        * `sudo mkdir -p /var/www/your_domain/html`
        * Assign ownership of the directory with the $USER environment variable, which should reference your current system user:
          * `sudo chown -R $USER:$USER /var/www/your_domain/html`
          * Grant reading permission to all the files inside the /var/www directory using the chmod command
            * `sudo chmod -R 755 /var/www/`
          * Create a sample index.html page to test the server block configuration
            * `sudo vim /var/www/your_domain/html/index.html`
            * Add the following into index.html
              * <pre>
                &lt;html&gt;
                    &lt;head&gt;
                      &lt;title&gt;Welcome to your_domain&lt;/title&gt;
                    &lt;/head&gt;
                    &lt;body&gt;
                      &lt;h1&gt;
                        Success! Your Nginx server is successfully configured for &lt;em&gt;your_domain&lt;/em&gt;.
                      &lt;/h1&gt;
                      &lt;p&gt;
                        This is a sample page.
                      &lt;/p&gt;
                    &lt;/body&gt;
                &lt;/html&gt;
                </pre>
            * Save and exit
      * Create a new server block at `/etc/nginx/sites-available/your_domain.conf`
        * Paste in the following configuration block into the file
          * <pre>
            html {
              server {
                listen 80;
                listen [::]:80;

                root /var/www/your_domain/html;
                index index.html index.htm index.php;

                server_name your_domain www.your_domain ip_address;

                location / {
                  # By default, Nginx buffers traffic for servers that it proxies for. Buffers improve server performance as a server response isn’t sent until the client finishes sending a complete response. To turn the buffer off.
                  # proxy_buffering off;
                  try_files $uri $uri/ =404;
                }

                # Setting up php within Nginx
                location ~ \.php$ {
                  try_files $uri =404;
                  fastcgi_intercept_errors on;
                  fastcgi_index  index.php;
                  include        fastcgi_params;
                  fastcgi_param  SCRIPT_FILENAME  $document_root$fastcgi_script_name;
                  fastcgi_pass   php-fpm;
                }

                # Error page 404
                # error_page 404 /404.html;
                #  location = /40x.html {
                # }

                # Error page 500 502 503 504
                # error_page 500 502 503 504 /50x.html;
                #  location = /50x.html {
                # }
              }

              include /etc/nginx/sites-enabled/*.conf
              server_names_hash_bucket_size 64;
            }
            </pre>
        * Save and exit
      * Test Nginx
        * `sudo nginx -t`
      * Restart Nginx Service
        * `sudo systemctl restart nginx`
      * Update your server’s SELinux security contexts so that Nginx is allowed to serve content from the `/var/www/your_domain directory`.
        * The following command will allow your custom document root to be served as HTTP content
          * `chcon -vR system_u:object_r:httpd_sys_content_t:s0 /var/www/your_domain/`
      * Now you can test your custom domain setup by navigating to http://your_domain, where you will see something like this:
      * Test PHP and Nginx
        * Create a new PHP file
          * `sudo vim /var/www/your_domain/html/hello.php`
        * Append the following PHP code
          * <pre>
            &lt;?php
              echo "Hello, world!\n";
            ?&ft;
            </pre>
        * Save and exit
        * One can also use the curl command to get same info using the cli
          * `curl -I http://<ip_address>/hello.php`
          * `curl http://<ip_address>/hello.php`
        * Create a PHP Info page
          * `sudo vim /var/www/your_domain/html/phpinfo.php`
        * Append the following PHP code
          * <pre>
            &lt;?php
              phpinfo();
            ?&ft;
            </pre>
        * Save and exit
        * Open a web browser and type the following url:
        * http://your-domain-OR-ip/hello.php
        * http://your-domain-OR-ip/phpinfo.php
