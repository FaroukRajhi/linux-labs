Let's thing what happens when we use a command such as su.
This let's us login as the root user, to allow that login the program asks us for the root password.
With this password, we prove to the application that we are authorized to perform this action.
In other words, we authenticate to the su command.
Authentication is a way to prove identity.
Once we're successfully authenticated, we^re allowed to do something.
Now we get a PAM: is short for Pluggable Authentication Modules.
This is a system that let's us plug in authentication modules.
This gives us a lot of flexibility to determine how we want certain utilities to perform authentication on our system.

With pluggable authentication modules, we can tell the su utility to authenticate us in a different way.
For example, we could make it allow us to login as root, but only if a special USB stick is plugged into the server.

Where are PAM related files stored?
We can find these in the /etc/pam.d directory.
We'll notice an interesting file here called su.
This is the file that defines the Pluggable Authentication Modules that should be used by the su utility.

Let's edit it and see what's inside.

================================================================
#The PAM configuration file for the Shadow `su' service


#This allows root to su without passwords (normal operation)
auth       sufficient pam_rootok.so

#Uncomment this to force users to be a member of group wheel
#before they can use `su'. You can also add "group=foo"
#to the end of this line if you want to use a group other
#than the default "wheel" (but this may have side effect of
#denying "root" user, unless she's a member of "foo" or explicitly
#permitted earlier by e.g. "sufficient pam_rootok.so").
#(Replaces the `SU_WHEEL_ONLY' option from login.defs)
#auth       required   pam_wheel.so
#Uncomment this if you want wheel members to be able to
#su without a password.
#auth       sufficient pam_wheel.so trust
#Uncomment this if you want members of a specific group to not
#be allowed to use su at all.
#auth       required   pam_wheel.so deny group=nosu
#Uncomment and edit /etc/security/time.conf if you need to set
#time restrainst on su usage.
#(Replaces the `PORTTIME_CHECKS_ENAB' option from login.defs
#as well as /etc/porttime)
#account    requisite  pam_time.so
#This module parses environment configuration file(s)
#and also allows you to use an extended config
#file /etc/security/pam_env.conf.
#
#parsing /etc/environment needs "readenv=1"
session       required   pam_env.so readenv=1
#locale variables are also kept into /etc/default/locale in etch
#reading this file *in addition to /etc/environment* does not hurt
session       required   pam_env.so readenv=1 envfile=/etc/default/locale

#Defines the MAIL environment variable
#However, userdel also needs MAIL_DIR and MAIL_FILE variables
#in /etc/login.defs to make sure that removing a user 
#also removes the user's mail spool file.
#See comments in /etc/login.defs

#"nopen" stands to avoid reporting new mail when su'ing to another user
session    optional   pam_mail.so nopen

#Sets up user limits according to /etc/security/limits.conf
#(Replaces the use of /etc/limits in old login)
session    required   pam_limits.so

#The standard Unix authentication modules, used with
#NIS (man nsswitch) as well as normal /etc/passwd and
#/etc/shadow entries.
@include common-auth
@include common-account
@include common-session
================================================================

Let's take a line and uncomment it:

#auth       sufficient pam_wheel.so trust
By uncommenting we actually plugged in an extra authentication module called "pam_wheel.so"
Whenever we use the su command, these authentication modules will be loaded in the order we see here.

sufficient: Once this authentication module gives the okay, then authentication is sufficient, job done
The rest of the modules after this line won't even be used if this module authenticates the user successfully.
Other example:

#auth       sufficient pam_wheel.so trust user_id

The first word (auth) establishes what type of authentication module this is.
This can be of the following types, it can be account, auth, password, or session.
You can get details about each one of those in the user manual for the PAM configuration files (man pam.conf).

A module like auth can also provide extra privileges after successful authentication.

A session module is used to prepare the user session in some way.
For example, after an auth module successfully let's us login, a session module could write into some log file, "the user $USER has successfully logged in at 8:02PM".

The next filed is the control field(sufficient, required, include, optional).
Required: This mean that users need to meet both conditions, ith they only provide a password, but no USB stuck the authentication fails
Sufficient: if the user had the USB stick plugged, the wouldn't even be asked for a password.


