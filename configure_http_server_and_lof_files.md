# We have the following Directory block in the main configuration file of httpd:


<Directory "/var/www/html/admin/">
</Directory>


Modify it to allow access to this directory from 127.0.0.1 IP address only.


Please make sure to restart httpd service after making the required changes.

Modify httpd main configuration:


sudo vi /etc/httpd/conf/httpd.conf



Add Require ip 127.0.0.1 line so that the whole block looks like this:


<Directory "/var/www/html/admin/">
  Require ip 127.0.0.1
</Directory>



Restart the httpd service.

sudo systemctl restart httpd

# Edit the correct configuration file to disable the mpm_event_module and enable the mpm_prefork_module instead.

/etc/httpd/conf.modules.d/00-mpm.conf file:


sudo vi /etc/httpd/conf.modules.d/00-mpm.conf



and make below given changes:


Uncomment LoadModule mpm_prefork_module modules/mod_mpm_prefork.so line.

LoadModule mpm_prefork_module modules/mod_mpm_prefork.so


Comment LoadModule mpm_event_module modules/mod_mpm_event.so line.

#LoadModule mpm_event_module modules/mod_mpm_event.so


# Edit the main config file of the httpd daemon and change the default listening port from 80 to 8090.

Edit /etc/httpd/conf/httpd.conf file:

sudo vi /etc/httpd/conf/httpd.conf



and search for Listen string, then change your port to 8090 and save the file:


Listen 8090


Restart the httpd service.

sudo systemctl restart httpd

# Edit the main config file of the httpd daemon and change what is collected in the error log. Currently, only warning-level errors, or worse are collected. Change it to debug level.

Edit /etc/httpd/conf/httpd.conf file:

sudo vi /etc/httpd/conf/httpd.conf



and search for LogLevel string, then make below given changes in the file.

LogLevel debug



Restart httpd service:

sudo systemctl restart httpd

# dit the main config file of the httpd daemon. Find this block: <Directory "/var/www/html">. In here, the Indexes and FollowSymLinks options are enabled for this directory.

Make the required changes to disable Indexes for this directory..

Edit /etc/httpd/conf/httpd.conf file:

sudo vi /etc/httpd/conf/httpd.conf



and search for Options Indexes FollowSymLinks line under <Directory "/var/www/html"> block and remove Indexes string from the line(it should look like as below) then save it:


Options FollowSymLinks



Restart httpd service:

sudo systemctl restart httpd

# Edit the main config file of the httpd daemon. Find this block: <Directory "/var/www/html">. Enable the use of .htaccess files in this directory. All types of overrides should be allowed in these files.

Edit /etc/httpd/conf/httpd.conf file:

sudo vi /etc/httpd/conf/httpd.conf



Search for AllowOverride under <Directory "/var/www/html"> block, change None to All then save the file:

AllowOverride None


Should become:

AllowOverride All



Now restart httpd service:

sudo systemctl restart httpd

# Modify the /var/www/html/admin/ Directory block in httpd main configuration file so that it looks like as below:


<Directory "/var/www/html/admin/">
    AuthType Basic
    AuthBasicProvider file
    AuthName "Secret admin page"
    AuthUserFile /etc/httpd/passwords
    Require valid-user
</Directory>


It enables password protection to this area of our website.


Create the password file i.e /etc/httpd/passwords and add the user called john with password john123 in the same.

Edit /etc/httpd/conf/httpd.conf file:

sudo vi /etc/httpd/conf/httpd.conf



Modify the /var/www/html/admin/ Directory block so that it looks like as below:


<Directory "/var/www/html/admin/">
    AuthType Basic
    AuthBasicProvider file
    AuthName "Secret admin page"
    AuthUserFile /etc/httpd/passwords
    Require valid-user
</Directory>



Execute below given command to create the password file and to add user in it:


sudo htpasswd -c /etc/httpd/passwords john



The above command will ask for user password twice, enter the given password once asked.


Restart httpd service:


sudo systemctl restart httpd


# Remove the user called john from the password file you created in the previous question.


sudo htpasswd -D /etc/httpd/passwords john

# Install the SSL module for httpd and enable it.

sudo dnf install mod_ssl -y



Once installed, the module should be enabled by default. To verify the same, execute below given command:


httpd -M  | grep ssl



You should see something like:


 ssl_module (shared)
