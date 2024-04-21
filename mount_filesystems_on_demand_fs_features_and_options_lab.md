# We learned about and how we can tell it to automatically mount something when a user tries to access a specific directory. In one of its configuration files we can add a line like this:

/etc/auto.master is the configuration file we need to edit.

# let's export /etc directory using NFS for 127.0.0.1 IP address. Also, the ro option should be applied, making this share read-only. Clients will only be able to read, but not write to this network shared directory.

Edit /etc/exports file:


sudo vi /etc/exports



add the required configuration:


/etc 127.0.0.1(ro)



reload nfs server:


sudo systemctl reload nfs-server