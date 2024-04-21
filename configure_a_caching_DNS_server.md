BIND is a popular application for hosting a DNS server.
Install from documentation
bind and bind-utils packages
Bind's main configuration file is located at /etc/named.conf
man named,conf to see more options.

configure bind server
vi /etc/named.conf
Check the documentation to understand the configurations.

# Maintain a DNS zone

DNS contains data domain name and its IP address.
A zone can group DNS data for a specific domain.
Add a zone for an example domain.
go to /etc/named.conf
go to the end of the file when we see zone block:
zone "." IN {

    type init;
    file "named.ca";
};

Add a zone for example.com

zone "example.com" IN{
    type master; => That signals that this the master data, the main information about the zone that can be found on the internet.
                => Is the source of the truth
                => Slave servers => can automatically synchronize with the master and keep a backup.
    file "example.com.zone";=> Point to the zone file
                            => Create a zone file in /var/named/named.localhost and copy it to example.com.zone
                            => Open it and configure TTL (time to live, 1D one day or H hour, and so on)
                            => Under $TTL type the domain name example.com     A  IP address

                            For more information check the documentation

}



