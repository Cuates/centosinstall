[Centos RHEL 8 Apache](https://certbot.eff.org/lets-encrypt/centosrhel8-apache)<br />
[Installing Snap On Red Hat](https://snapcraft.io/docs/installing-snap-on-red-hat)<br />
[How To Set Up Apache Virtual Hosts On Centos 8](https://linuxize.com/post/how-to-set-up-apache-virtual-hosts-on-centos-8/)<br />
[How To Enable HTTP 2 In Apache](https://www.howtoforge.com/how-to-enable-http-2-in-apache/)<br />
[How To Check If Website Has HTTP 2 Protocol Support](https://stackoverflow.com/questions/54091567/how-to-check-if-website-has-http-2-protocol-support)<br />
[Enable HTTP2 In Apache On Ubuntu](https://www.tecmint.com/enable-http2-in-apache-on-ubuntu/)<br />
[With HTTP3 On The Horizon Have You Upgraded To HTTP2](https://www.cloudsavvyit.com/2007/with-http-3-on-the-horizon-have-you-upgraded-to-http-2/)<br />
[How To Enable TLS 1.3 In Apache On CentOS 8](https://devopscraft.com/how-to-enable-tls-1-3-in-apache-on-centos-8/)

* Prerequisite
  * Apache/Httpd
    * [Apache/Httpd Web Server](https://github.com/Cuates/lampcentosinstall/tree/master/webserver)
  * NoIP
    * [Domain Name](https://github.com/Cuates/lampcentosinstall/tree/master/system/domainname)

* Set Apache virtual host before proceeding with Certbot
  * `sudo vim /etc/httpd/conf.d/<domain_name>.conf`
    * Paste the following into the file
      * <pre>
        &lt;VirtualHost *:80&gt;
          ServerName cuateslws.ddns.net
          ServerAlias cuateslws.ddns.net
          ServerAdmin webmaster@example.com
          DocumentRoot /var/www/html
          &lt;Directory /var/www/html
            Options FollowSymLinks
            AllowOverride None
            Order allow,deny
            Allow from all
          &lt;/Directory&gt;
          ErrorLog /var/log/httpd/cuateslws.ddns.net-error.log
          CustomLog /var/log/httpd/cuateslws.ddns.net-access.log combined
        &lt;/VirtualHost&gt;
        </pre>
  * Save and exit
  * Restart apache/httpd
    * `sudo systemctl restart httpd`
* Install SSH onto the server
* Install snapd
  * `sudo dnf -y install snapd`
  * The systemd unit that manages the main snap communication socket needs to be enabled
    * sudo systemctl enable --now snapd.socket
  * To enable classic snap support, enter the following to create a symbolic link between /var/lib/snapd/snap and /snap
    * `sudo ln -s /var/lib/snapd/snap /snap`
  * Either log out and back in again or restart your system to ensure snap’s paths are updated correctly.
* Ensure that your version of snapd is up to date
  * `sudo snap install core`
    * WAIT FOR THIS TO FINISH
  * `sudo snap refresh core`
* Remove any Certbot OS packages
  * `sudo dnf remove certbot`
* Install Certbot
  * `sudo snap install --classic certbot`
    * WAIT FOR THIS TO FINISH
* Prepare the Certbot command
  * `sudo ln -s /snap/bin/certbot /usr/bin/certbot`
* Choose how you'd like to run Certbot Either get and install your certificates
  * Run this command to get a certificate and have Certbot edit your Apache configuration automatically to serve it, turning on HTTPS access in a single step.
    * `sudo certbot --apache`
      * Enter your email address when prompted for urgent renewal and security notices
      * Enter A to agree to the terms and conditions when prompted
      * Choose Y or N when prompted to share your email address with the EFF
      * Choose 1 when prompted about which domain you want the certificate for (there should only be one)
        * If none were found, then proceed to add your domain name
          * No names were found in your configuration files. Please enter in your domain name(s) (comma and/or space separated)  (Enter 'c' to cancel): yourdomain
          * Created an SSL vhost at /etc/httpd/conf.d/<yourdomainname>-le-ssl.conf
            Deploying Certificate to VirtualHost /etc/httpd/conf.d/<yourdomainname>-le-ssl.conf
            Redirecting vhost in /etc/httpd/conf.d/<yourdomainname>.conf to ssl vhost in /etc/httpd/conf.d/<yourdomainname>-le-ssl.conf
          * Create a virutalhost first
          * Re-execute the command above
    * IMPORTANT NOTES:
      - Congratulations! Your certificate and chain have been saved at:
        /etc/letsencrypt/live/\<yourdomainname\>/fullchain.pem
        Your key file has been saved at:
        /etc/letsencrypt/live/\<yourdomainname\>/privkey.pem
        Your cert will expire on 2021-01-12. To obtain a new or tweaked
        version of this certificate in the future, simply run certbot again
        with the "certonly" option. To non-interactively renew *all* of
        your certificates, run "certbot renew". You should make a
        secure backup of this folder now. This configuration directory will
        also contain certificates and private keys obtained by Certbot so
        making regular backups of this folder is ideal.
  * Or, just get a certificate
    * `sudo certbot certonly --apache`
* Test automatic renewal
  * `sudo certbot renew --dry-run`
  * The command to renew certbot is installed in one of the following locations:
    /etc/crontab/
    /etc/cron.*/*
    systemctl list-timers
* Add Protocols h2 (HTTP/2) to the port 443 Certbot generated file
  * `sudo vim /etc/httpd/conf.d/<domain_name>-le-ssl.conf`
    * Paste the HTTP/2 section into the below file
      * <pre>
        &lt;IfModule mod_ssl.c&gt;
          &lt;VirtualHost *:443&gt;
            ServerName &lt;domain_name&gt;
            ServerAlias &lt;domain_name&gt;
            ServerAdmin webmaster@example.com
            DocumentRoot /var/www/html
            &lt;Directory /var/www/html&gt;
              Options FollowSymLinks
              AllowOverride None
              Order allow,deny
              Allow from all
            &lt;/Directory&gt;
            ErrorLog /var/log/httpd/&lt;domain_name&gt;-error.log
            CustomLog /var/log/httpd/&lt;domain_name&gt;-access.log combined
            # Enable HTTP/2, if available
            Protocols h2 http/1.1
            SSLCertificateFile /etc/letsencrypt/live/&lt;domain_name&gt;/fullchain.pem
            SSLCertificateKeyFile /etc/letsencrypt/live/&lt;domain_name&gt;/privkey.pem
            Include /etc/letsencrypt/options-ssl-apache.conf
          &lt;/VirtualHost&gt;
        &lt;/IfModule&gt;
        </pre>
  * Save and exit
  * Test the apache configuration
    * `sudo apachectl configtest`
  * Restart apache/httpd
    * `sudo systemctl restart httpd`
  * Test HTTP/2 Protocol
    * `curl -I --http2 -s https://<domain_name>/ | grep HTTP`
      * A message of HTTP/2 200 will display
      * Else a message of HTTP/1.1 200 OK if HTTP/2 did not work
* Visit your router setting for port forwarding
  * Set the IP address to the port 443 in the port forwarding section of your router
* Confirm that Certbot worked
  * Navigate to your site using the https prefix
    * e.g. https://yourdomainname
