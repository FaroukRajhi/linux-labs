When we have a lot of users logging in the system, we may want to impose limits on what resources they can use.
This way we can ensure that user A does not use 80% of the CPU, leaving very little to spare for the others.
To set such a limit, we can edit this file: "sudo vim /etc/security/limits.conf"
We will see this:

#<domain>      <type>  <item>         <value>
#

#*               soft    core            0
#root            hard    core            100000
#*               hard    rss             10000
#@student        hard    nproc           20
#@faculty        soft    nproc           20
#@faculty        hard    nproc           50
#ftp             hard    nproc           0
#ftp             -       chroot          /ftp
#@student        -       maxlogins       4
sonarqube   -   nofile   65536
sonarqube   -   nproc    4096
#End of file

We can see that the syntax for setting a limit: domain, type item and value.
Let's break this down.

1. domain: We specify three things
username, group name (starts with "@")
"*" match everything=> for every user on the system

2. type: 
Which can be three different values;
**hard**: cannot be overwritten by a regular user.
If a hard limit says they can only run 30 processes, they cannot go above that
**soft**: Instead of a max value, this is more like the startup limit.
If a user has a soft limit of maximum processes and hard limit of 20, the following happens:
When they log in the limit will be set to 10 processes, but if the user has some temporary need to increase this, thy can raise to 11, 12, 15 even 20 processes.
They can get a slight increase when absolutely required.
manually raise
**dash(-)**: 
This specifies that this is both a hard limit and a soft limit.
We saying user should be able to run 20 processes at the most.
When he logs in, he should be able to use up to his entire allocation without needing to manually raise his limit.

3. item:
This decides what this limit is for.
We can have things such as:
**nproc**: set the maximum number of processes that can be open in a user session.
**fsize**: set the maximum file size that can be created in this user session, the size is in kilobytes.
**cpu:**sets the limits per cpu time, specifies in minutes, so when a process uses 100% of a cpu core for one second, it will use up one second of its allocated time.
if it uses 50% of one core or one second it will use up 0.5 seconds of its allocation

For more information check manual using "man limit.conf"



