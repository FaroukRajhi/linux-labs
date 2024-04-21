visudo
%wheel ALL=(ALL)      ALL
**%wheel :** group or users
**ALL:** Is the host field. 
Here we can specify that these rules only apply if our server's host name, or IP address has a specific value
**(ALL):** Is the run as field.
Here we could type a list of usernames.

**Third ALL**: 
user/group host=(run_as_user) command_list

user ALL=(ALL) /bin/ls, /bin/stat