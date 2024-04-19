# Identify what % space of / partition is in use on our system. Save the value in /home/bob/used file.


For example if used space is 10% then the file content should be 10%
df /

# Figure out how much storage space the /bin/ directory is using and save the value in /home/bob/bin file.

du -sh /bin/

# Use the correct command to check out the memory on this system (in megabytes). In /home/bob/memory file, save the total amount of RAM that this system has.

free --mega

# Use the correct command to identify the CPU core(s) per socket on this system. Save its value in /home/bob/cpu file.

lscpu

# On /dev/vdb we have an XFS filesystem. Use the correct command to check this filesystem for errors 
sudo xfs_repair /dev/vdb 
