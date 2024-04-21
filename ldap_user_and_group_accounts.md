By default, Linux keeps information about user accounts and groups stored locally.
In /etc/passwd

The problem is that we usually have to manage hundreds of servers.
And so keeping track of what user accounts and groups exit on each system can be a hassle even with automation tools like ansible, especially if we have constantly need to create new user accounts, remove unused users, define new groups, and so on.

Example: we want to create a new user account and configured to 200 servers
All we need to do is add an LDAP server into the mix.
We can configure our Linux system to use an LDAP server as an additional source of information for user and group accounts.
So whenever we need to add, remove, or modify user accounts and groups, we avoid having to make changes on hundreds of individual servers.
All we need to do is update data about these accounts on a single central location on the LDAP server.
In our linux server, we'll get the updated data about users and groups accounts automatically.

