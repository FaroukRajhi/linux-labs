IMAP is short for internet Message Access Protocol.
Its daemon used on Linux is Dovecot.
At the servers, an email outlook.com logs on Dovecot.
IMAP does not encrypt data we use IMAPS instead. 
Check the documentation for more information and how to install it.

###### Lab #######

# What file do we edit to add a new email alias?

We need to edit /etc/aliases file to add a new email alias.

# What command do we use to inform our email daemon that our aliases have changed?

We can use sudo newaliases command to inform our email daemon that our aliases have changed.

# Install postfix email server and mailx email client on this system. Also make sure to start postfix service.

Execute below given command


sudo dnf install postfix mailx -y



Now start postfix service:


sudo systemctl start postfix


# Our system is configured to receive emails sent to <username>@example.com.


Send an email to user john from user bob and make sure the subject of the email is Hi John

You can write anything in the body of the email.


echo "This is a test email" | mailx -s "Hi John" john

# Create an alias that takes all emails received at bob@example.com and forwards it to john@example.com.

Edit /etc/aliases file:

sudo vi /etc/aliases



Add below given line in it:

bob: john



Save and exit.


Refresh the new aliases:


sudo newaliases

# Change Dovecot's configuration and disable SSL/TLS encryption.


Make sure to restart dovecot's service after making the required changes.

Edit /etc/dovecot/conf.d/10-ssl.conf file:

sudo vi /etc/dovecot/conf.d/10-ssl.conf



Change ssl parameter value to no:

ssl = no



Save and exit.


Now restart dovecot service, Please note that service can take few seconds to restart:


sudo systemctl restart dovecot

# Can you figure out in what Dovecot config file we can find quota related settings? Edit that config file and make sure that the maximum accepted mail size is set to 200M.

Edit /etc/dovecot/conf.d/90-quota.conf file:

sudo vi /etc/dovecot/conf.d/90-quota.conf



Modify below line in this file. Make sure you uncomment this line:


quota_max_mail_size = 200M

