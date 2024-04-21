# Create an xfs filesystem with the label "DataDisk" on /dev/vdb.

sudo mkfs.xfs -L "DataDisk" /dev/vdb

# Create an ext4 filesystem with a number of 2048 inodes on /dev/vdc.

mkfs.ext4 -N 2048 /dev/vdc

# Mount /dev/vdb in the /mnt/ directory.

sudo mount /dev/vdb /mnt

# Configure the system to automatically mount /dev/vdc when it boots up. This partition has an ext4 filesystem on it. It should mount the filesystem to the /test directory. This directory does not exist, make sure you create it first.

First create a directory using following command:

sudo mkdir /test


Edit /etc/fstab file:

sudo vi /etc/fstab



Add this line in it:

/dev/vdc /test ext4 defaults 0 2

# Configure the system to automatically use /dev/vdb as swap when it boots up.

sudo vi /etc/fstab



Add this line in it:

/dev/vdb none swap defaults 0 0

