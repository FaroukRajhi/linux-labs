# Edit the mariadb-server.cnf config file to enable the remote access to your MariaDB server.

sudo vi /etc/my.cnf.d/mariadb-server.cnf
Uncomment below given line, so that it looks like as below:


bind-address=0.0.0.0



Restart maridb service:


sudo systemctl restart mariadb

# Through any method you want, change the password for the MariaDB root user to Secu43@123.

sudo mysql_secure_installation
mysql -u root -p

# Update the MariaDB server config file to change the error logs file to /var/log/mariadb/server_mariadb.log

udo vi /etc/my.cnf.d/mariadb-server.cnf



Update below given line, so that it looks like as below:


log-error=/var/log/mariadb/server_mariadb.log



Restart maridb service:


sudo systemctl restart mariadb

# Change the MariaDB server port to 3308

sudo vi /etc/my.cnf.d/mariadb-server.cnf



Add below given line under [mysqld]:


port=3308



Restart mariadb service:


sudo systemctl restart mariadb

# We have virsh utility installed that let us interact with virtual machines and qemu-kvm installed that let us create and run them.

Check if any virtual machine is present on this system (stopped or running), 

sudo virsh list --all


#  start this VM.
sudo virsh start VM1

# Now completely remove the VM1 virtual machine.

sudo virsh destroy VM1
sudo virsh undefine VM1

# Create a virtual machine using this configuration file, and make sure to start it.

<domain type="qemu">
  <name>VM2</name>
  <memory unit="MiB">125</memory>
  <vcpu>1</vcpu>
  <os>
    <type arch='x86_64'>hvm</type>
  </os>
</domain>
sudo virsh define /path/to/testmachine2.xml

# Right now, when we start up or reboot this system, the virtual machines on it have to be manually started.
But we want VM2 virtual machine to start up automatically at boot.

sudo virsh autostart VM2

# Change the memory size for VM2, set its value to 80M


Make sure the changes are in effect, you can verify the same using sudo virsh dominfo VM2 command.

Execute below given command to change the maximum memory size:


sudo virsh setmaxmem VM2 80M --config



Execute below given command to change the memory size as needed:


sudo virsh setmem VM2 80M --config



Shutdown the VM:


sudo virsh shutdown VM2
