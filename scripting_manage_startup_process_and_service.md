# Make sure rpcbind.service unit automatically starts up after Linux boots.

sudo systemctl enable rpcbind.service

# Create a script called script.sh. This script should create a tar archive called archive.tar.gz. The script should archive the directory called dir1

vi script.sh

#!/bin/bash
tar acf archive.tar.gz dir1

chmod u+x script.sh

# There is a service unit that automatically starts up the SSH daemon. Use the correct command to find out the PID assigned to the process launched by this service.


Save the PID in /home/bob/pid file.

systemctl status sshd.service
vi /home/bob/pid
134