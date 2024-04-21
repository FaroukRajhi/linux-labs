# Edit the configuration of the SSH server and disable password logins.


Please make sure to restart the sshd service after making the required changes.

Edit /etc/ssh/sshd_config file:


sudo vi /etc/ssh/sshd_config



Uncomment below given line or add it if doesn't exist:


PasswordAuthentication no


Save your changes and restart sshd service:


sudo systemctl restart sshd

# Edit the system-wide configuration of the SSH client and turn on X11 forwarding.

Edit /etc/ssh/ssh_config file:

sudo vi /etc/ssh/ssh_config



Uncomment below given line or add it if doesn't exist:


ForwardX11 yes

# Install squid proxy server on this system and start its service.

Execute below given command to install the required package:


sudo dnf -y install squid



Start squid service


sudo systemctl start squid

# Edit the config file of the Squid proxy daemon. Modify it to deny access to the IP addresses defined in the ACL called localnet

Edit /etc/squid/squid.conf file:

sudo vi /etc/squid/squid.conf



And change http_access allow localnet line to http_access deny localnet

# Edit the configuration of the Squid proxy daemon. Add a src type acl and name it vpn. The IP you should use in this acl is 203.0.110.5. Now add a new rule that tells the proxy server to allow access to the acl named vpn.

Edit /etc/squid/squid.conf file:

sudo vi /etc/squid/squid.conf



and save below given changes in it:


Add this line

acl vpn src 203.0.110.5



Add below given line in the same file before http_access deny all line:

http_access allow vpn

# Edit the configuration of the SSH server and configure it to use only IPv4 IP address family.



Edit /etc/ssh/sshd_config file:

sudo vi /etc/ssh/sshd_config



Uncomment the below given line in it:

#AddressFamily any



and change it to (add it if doesn't exist):

AddressFamily inet

# Edit the configuration of the Squid proxy daemon. Now add a new rule that allow http access to the external

Edit /etc/squid/squid.conf file:

sudo vi /etc/squid/squid.conf



Add below given line in this file after http_access allow localhost line:

http_access allow external

# Edit the configuration of the Squid proxy daemon , add an acl and http access rule to block facebook.com.

Edit /etc/squid/squid.conf file:

sudo vi /etc/squid/squid.conf



Add below given acl:


acl facebook dstdomain .facebook.com



And add below given line after http_access allow localhost line:


http_access deny facebook

# Edit the configuration of the SSH server and re-enable password logins, but disable the SSH login for user root.

Edit /etc/ssh/sshd_config file:


sudo vi /etc/ssh/sshd_config



Change below given line:


PasswordAuthentication no



to


PasswordAuthentication yes


Uncomment below given line or add it if doesn't exist:


PermitRootLogin no


Save your changes and restart sshd service:

# In configuration file of the SSH server, change the maximum number of authentication attempts permitted per connection to 4

Edit /etc/ssh/sshd_config file:


sudo vi /etc/ssh/sshd_config



Uncomment below given line or add it if doesn't exist:


MaxAuthTries 4


Save your changes and restart sshd service:


sudo systemctl restart sshd



