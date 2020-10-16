[Centos RHEL 8 Apache](https://certbot.eff.org/lets-encrypt/centosrhel8-apache)<br />
[Installing Snap On Red Hat](https://snapcraft.io/docs/installing-snap-on-red-hat)<br />
[How To Set Up Apache Virtual Hosts On Centos 8](https://linuxize.com/post/how-to-set-up-apache-virtual-hosts-on-centos-8/)

* Prerequisite
  * Apache/Httpd
    * [Apache/Httpd Web Server](https://github.com/Cuates/lampcentosinstall/tree/master/webserver)
  * NoIP
    * [Domain Name](https://github.com/Cuates/lampcentosinstall/tree/master/system/domainname)

* Set Apache virtual host before proceeding with Certbot
  * `sudo vim /etc/httpd/conf.d/<domain_name>.conf`
    * Paste the following into the file
      * `<VirtualHost *:80>`<br />
        `    ServerName cuateslws.ddns.net`<br />
        `    ServerAlias cuateslws.ddns.net`<br />
        `    ServerAdmin webmaster@example.com`<br />
        `    DocumentRoot /var/www/html`<br />
        `    <Directory /var/www/html>`<br />
        `        Options FollowSymLinks`<br />
        `        AllowOverride None`<br />
        `        Order allow,deny`<br />
        `        Allow from all`<br />
        `    </Directory>`<br />
        `    ErrorLog /var/log/httpd/cuateslws.ddns.net-error.log`<br />
        `    CustomLog /var/log/httpd/cuateslws.ddns.net-access.log combined`<br />
        `</VirtualHost>`
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
** Add Protocols h2 (HTTP/2) to the port 443 Certbot generated file
  * `sudo vim /etc/httpd/conf.d/<domain_name>-le-ssl.conf`
    * Paste the following into the file
      * `<IfModule mod_ssl.c>`<br />
        `<VirtualHost *:443>`<br />
        `    ServerName <domain_name>`<br />
        `    ServerAlias <domain_name>`<br />
        `    ServerAdmin webmaster@example.com`<br />
        `    DocumentRoot /var/www/html`<br />
        `    <Directory /var/www/html>`<br />
        `        Options FollowSymLinks`<br />
        `        AllowOverride None`<br />
        `        Order allow,deny`<br />
        `        Allow from all`<br />
        `    </Directory>`<br />
        `    ErrorLog /var/log/httpd/<domain_name>-error.log`<br />
        `    CustomLog /var/log/httpd/<domain_name>-access.log combined`<br />
        `    # Enable HTTP/2, if available`<br />
        `    Protocols h2 http/1.1`<br />
        `SSLCertificateFile /etc/letsencrypt/live/<domain_name>/fullchain.pem`<br />
        `SSLCertificateKeyFile /etc/letsencrypt/live/<domain_name>/privkey.pem`<br />
        `Include /etc/letsencrypt/options-ssl-apache.conf`<br />
        `</VirtualHost>`<br />
        `</IfModule>`
  * Save and exit
  * Restart apache/httpd
    * `sudo systemctl restart httpd`
* Visit your router setting for port forwarding
  * Set the IP address to the port 443 in the port forwarding section of your router
* Confirm that Certbot worked
  * Navigate to your site using the https prefix
    * e.g. https://yourdomainname
