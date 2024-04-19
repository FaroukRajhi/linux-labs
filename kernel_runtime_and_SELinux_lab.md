# Find the SELinux labels of sshd process running on this system
ps auxZ | grep sshd

For example if the context is system_u:system_r:initrc_t:s0

# Turn on kernel.modules_disabled kernel runtime parameter, so that loading new kernel modules will be disabled.

sudo sysctl -w kernel.modules_disabled=1

# Check out the SELinux label for the file stored at /bin/sudo

ls -Z /bin/sudo
You should see sudo_exec_t in the output

# Use the sysctl command to make sure this kernel runtime parameter is actively enabling its settings:

sudo sysctl -w net.ipv6.conf.lo.seg6_enabled=1

# Adjust the value of this kernel runtime parameter, vm.swappiness, to 10.

After you set this to 10, also make the change persistent so that it will be auto-set to this value on the next reboot.

sudo vi /etc/sysctl.conf
vm.swappiness=10
sudo sysctl -p

# Change the SELinux context of /var/index.html file to httpd_sys_content_t

sudo chcon -t httpd_sys_content_t /var/index.html

# Temporarily change the SELinux status to Permissive on this system.

sudo setenforce 0

# Identify the SELinux Roles for xguest_u SELinux user 
sudo semanage user -l
