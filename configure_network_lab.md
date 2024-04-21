# Find out what process is listening for incoming connections on port 22, and identify its PID.

sudo ss -tlnp | grep :22

# Now, find out what process is listening for incoming connections on port 53, and identify its PID.

sudo ss -tlnpu | grep :53

# So now let's try to identify the process name based on the port it's listening on, find out the process name that is listening for incoming connections on port 8080.

sudo netstat -natp | grep :8080

# Use the ip command to add a temporary extra IP to the eth1 interface. You should add the CIDR notation of the IP: 192.168.9.3/24.

sudo ip a add 192.168.9.3/24 dev eth1

# Create the following Netplan config in the file name 99-custom.yaml under /etc/netplan directory.

sudo vim 99-custom.yaml
network:
  version: 2
  ethernets:
    enp6s0:
      dhcp4: false
      dhcp6: false
      addresses:
        - 10.0.10.5/24

sudo chmod 600 /etc/netplan/99-custom.yaml
sudo netplan apply

# The interface named enp6s0 is configured with a permanent IP 10.0.10.5/24. Change this configuration so that the permanent IP is 192.168.10.10/24 instead of 10.0.10.5/24.

Update the file /etc/netplan/99-custom.yaml created in the previous step using the vim command shown below.

network:
  version: 2
  ethernets:
    enp6s0:
      dhcp4: false
      dhcp6: false
      addresses:
        - 192.168.10.10/24
sudo netplan try
sudo netplan apply



