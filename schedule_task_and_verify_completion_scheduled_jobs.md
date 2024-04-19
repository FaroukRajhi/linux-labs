# 0 3 15 * * /usr/bin/touch test_passed

On the 15th of each month, at 3 AM

# We're logged in as the user called alex. How do we see the crontab for theroot user?

Using sudo crontab -l command we can see the crontab for theroot user.




# What is the command to see the jobs that are scheduled to run in at utility?

atq

# Remove all at jobs that exist for the user bob.
Identify the jobid using atq command:
Remove the job using jobid, for example if jobid is 3 then execute below given command :
atrm <job id>

# Add this command to the crontab of root:


/usr/bin/touch test_passed


Make it run every day at 21:30

30 21 * * * /usr/bin/touch test_passed

# Add an anacron job with the following specifications:


A. It should run once every 10 days

B. It should have 5 minutes of delay

C. The job id should be db_cleanup

D. The command to run is: /usr/bin/touch /root/anacron_created_this

10 5 db_cleanup /usr/bin/touch /root/anacron_created_this

# Using crontab utility add a cron for user root to run below given command:


/usr/bin/touch monthly



Make it run at 12:00AM on the 1st of every month.
0 0 1 * * /usr/bin/touch monthly

# Using crontab utility add a cron for user root to run below given command:


/usr/bin/touch weekly



Make it run at 11:00AM on every Sunday.
0 11 * * 0 /usr/bin/touch weekly
# Add a cron for bob user to execute sudo systemctl restart nginx command on Sundays every week at 6am and 11pm.

0 6,23 * * 0 sudo systemctl restart nginx





