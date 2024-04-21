# Install bind DNS server on this system.

sudo dnf install bind bind-utils -y

# Configure the Bind daemon to accept queries from any IP on the Internet. Make sure to start named service after making required changes in the configuration.

Edit /etc/named.conf file:

sudo vi /etc/named.conf



Add below given line in it under recursing-file  "/var/named/data/named.recursing"; line

allow-query    { 0.0.0.0/0; };



Start named.service:

sudo systemctl start named.service

# We have added a new zone file /var/named/example.com.zone which contains DNS configuration for example.com domain.
Query the local DNS server and identify the current A record value for example.com domain. 

dig @localhost example.com
Under ANSWER SECTION note down the IP address for A record, you will see an output something like this:


example.com.            86381   IN      A       93.184.216.34

# Modify /var/named/example.com.zone and add a new entry so that this subdomain


database.example.com


has this IP address: 1.2.3.4


Don't forget to restart the named.service after you've made your change.

Edit /var/named/example.com.zone file:

sudo vi  /var/named/example.com.zone



and add below given line in it:

database                A       1.2.3.4



Then restart named.service using below given command:

sudo systemctl restart named.service

# Modify /var/named/example.com.zone and make mysql.example.com an alias for database.example.com by adding the proper CNAME entry. Otherwise said, mysql.example.com should point to database.example.com. Restart the named.service after you've added the new entry.

Edit /var/named/example.com.zone file:

sudo vi  /var/named/example.com.zone



Add below given line in it:

mysql.example.com.      CNAME   database.example.com.



Then restart named.service using below given command:

sudo systemctl restart named.service

# By default the bind server also fetches DNS data from other DNS servers on the Internet, when it does not have it available in its own cache. But somehow our bind server is not able to query the kodekloud.com domain data.

Edit /etc/named.conf file:


sudo vi /etc/named.conf



Look for recursion and make sure its value is set to yes


recursion yes;



Then restart named.service using below given command:

sudo systemctl restart named.service

# Change the TTL for example.com domain to tell other DNS servers that, they may query our zone to cache this data for 2 hours.

Edit /var/named/example.com.zone file:


sudo vi /var/named/example.com.zone



In the beginning of the file change $TTL value from 1H to 2H


$TTL 2H



Then restart named.service using below given command:

sudo systemctl restart named.service

