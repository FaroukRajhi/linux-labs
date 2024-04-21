# How do we format a partition as swap space?

We can format a partition as swap space using sudo mkswap /dev/vdb3 command. Where /dev/vdb3 is the partition we want to format.

# Find out the swapfile used on this system

swapon --show

# Create three primary partitions on /dev/vdb.


First should have 10MB, second should have 21MB and the third should have 15MB.

Follow below given steps:

sudo fdisk /dev/vdb



Now enter below given responses:

Command (m for help): n
Select (default p):  <just-leave-it-default-and-press-enter>
Partition number (1-4, default 1): <just-leave-it-default-and-press-enter>
First sector (2048-2097151, default 2048):  <just-leave-it-default-and-press-enter>
Last sector, +sectors or +size{K,M,G,T,P} (2048-2097151, default 2097151): +10M
Command (m for help): w
You can follow these same steps for all three partitions.


Further you can verify the created partitions using below given command:

lsblk

# Delete the 10MB partition.

Follow below given steps:

sudo fdisk /dev/vdb



Now enter below given responses:

Command (m for help): d
Partition number (1-3, default 3): 1
Command (m for help): p
Command (m for help): w



Further you can verify the remaining partitions using below given command:

lsblk

# Format the 21MB partition as swap. Next, make it active, tell Linux to start using it as swap memory.

Execute below given commands:

sudo mkswap /dev/vdb2
sudo swapon /dev/vdb2



You can validate with:

sudo swapon --show

# Tell Linux to stop using the 21MB partition as swap.

Execute below given command:

sudo swapoff /dev/vdb2



You can validate with:

sudo swapon --show

# Increase the existing swap (i.e /swapfile) size by 1GB.

Execute below given command:


sudo dd if=/dev/zero of=/swapfile bs=1M count=1024 oflag=append conv=notrunc



In this command /swapfile is the swap file you are going to edit and count=1024 is the exact increase in size.


Disable the swap file:


sudo swapoff /swapfile



Setup the file as a swap file again.


sudo mkswap /swapfile



Enable again swaping:

sudo swapon /swapfile

# Resize the /dev/vdb3 partition (which you created earlier) to 21MB.

Run below given command:


sudo cfdisk /dev/vdb



You will see some details as below (it can vary from one system to another):


Device             Boot                  Start            End        Sectors         Size        Id Type
>>  Free space                                2048          22527          20480          10M                             
    /dev/vdb2                                22528          65535          43008          21M        83 Linux
    /dev/vdb3                                65536         108543          43008          21M        83 Linux
    Free space                              108544        2097151        1988608         971M



Using arrow keys, select the partition you want to resize, in our case it's /dev/vdb3. In the bottom you will see some options as below:


[Bootable]  [ Delete ]  [ Resize ]  [  Quit  ]  [  Type  ]  [  Help  ]  [  Write ]  [  Dump  ]



Using arrow keys, select the Resize option and press Enter and adjust the size as needed. For example in our case we will set it to 21M and then press Enter again.


New size: 21M



Now using arrow keys, select the Write option and press Enter. It will ask for the confirmation so enter Yes and press Enter


Are you sure you want to write the partition table to disk? yes



Now using arrow keys, select the Quit option and press Enter. You are done!!


You can confirm your changes by listing the partitions using lsblk command.