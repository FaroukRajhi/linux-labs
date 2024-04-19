# SELinux Context

unconfined_u:object_r:user_home_t:s0

unconfined_u = user
object_r = role
user_home_t = type
s0 = level

To allow or deny some action, SELinux roughly follows this logic.
SELinux has a policy configuration which we will see in a bit, where the user and their roles are defined.

The user is not the same as the username you log in with, it's an SELinux user.
Every linux user who logs into a system is mapped to an SELinux user as part of the SELinux policy configuration.

Map of the user is identified, a decision is made to see if it can assume the role.
Each user can only assume a predefined set of roles.

For example, we could imagine how a developer_u should only be able to enter roles like developer_r or docker_r that allow them to read and write application code, launch docker containers, and so on.

They should not be able to enter roles like cisadmin_r that let them change system settings.

If role can be entered, next a check is performed to see it this role transition to the type.

The type of the name of this field comes from type enforcement, and this type is like a protective software jail.
Once something enters the type enforcement defined here, it can only do certain things and nothing else.

This restriction bubble is called "type" when dealing with files and "domain" when dealing with processes.
=============================================
SELinux user        Roles
=============================================

developer_u         developer_r, docker_r
guest_u             guest_r
root                staff_r,sysadm_r,system_r
==============================================

# The path of security module achieves
1. It makes sure that only certain users can enter certain roles and certain types.
=> It keeps unauthorized users and processes from entering types and domains that are not for them.
2. It lets authorized users and processes do their job, by granting the permissions they need
3. Authorized users and processes are allowed to take "only" a limited set of actions.
4. Everything else is denied

Example:
It can protect against a hijacked program.
Imagine a hacker takes control of the Apache program that serves web pages to our websites visitors.
They're still restricted to the SELinux domain, so they aren't able to step out of those boundaries.
They're effectively in a virtual jail, and the damage they can do thus is greatly reduced.


The most important part of the SELinux context is the type or domain and that's the third part of our label.
Also the level is almost never actively used on a regular system.

To see all processes, we use ps ax and add security labels to our view by using Z.
From that we can see our a process running here and spot that's restricted to the "type" domain
This domain contains a strict set of policies that define what the process is allowed to do.
Also, important to note that not anything can enter the type_t (ex. sshd_t) domain.
In this case, only files that have the same type_t  in their label can enter this domain.
Sure enough, if we check the file containing the SSHD program:
"ls -Z /usr/sbin/sshd
system_u:object_r:sshd_exec_t:s0 /usr/sbin/sshd.

To see the security context assigned to our current user use:
id -Z

Check the documentation for more information