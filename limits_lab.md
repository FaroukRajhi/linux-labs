# Modify the security limits file and make sure that the user called trinity can run no more than 30 processes in her session.
This should be both a hard limit and a soft limit, written in a single line.

sudo vi /etc/security/limits.conf
trinity - nproc 30

# Identify all the security limits currently applied in our user's session

ulimit -a

# Modify the sudoers file in such a way to allow the user called trinity to run any sudo command without needing to provide her password.

sudo visudo /etc/sudoers
trinity    ALL=(ALL)   NOPASSWD: ALL
# Modify the sudoers file again. Remove your previous entry for the user called trinity if it still exists.
Now add a new entry that allows trinity to only run the /usr/bin/mount command with sudo.

trinity ALL=(ALL) /usr/bin/mount

# Make changes in security limits file for user stephen so that he can create maximum filesize upto 4 MiB. This should be a hard limit.

sudo vi /etc/security/limits.conf
stephen hard fsize 4096

# Set a soft limit of 20 processes for everyone in the salesteam group.

sudo vi /etc/security/limits.conf
@salesteam     soft    nproc     20

# Define a policy for all the users in the salesteam group to run any sudo command.

sudo visudo /etc/sudoers
%salesteam     ALL=(ALL)     ALL


# Define a policy, so that user trinity be able to run sudo commands as the user sam.

trinity   ALL=(sam)   ALL

