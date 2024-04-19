# Assign a nice value of 9 to the sshd process.

ps aux
sudo renice 9 <PID>

# List all files that are opened by process with PID 1, this process is owned by the root user.
sudo lsof -p 1 > /home/bob/files.txt

# Search the logs for entries related to the SSH daemon i.e sshd. Find out what IP address last connected to this daemon successfully.
sudo journalctl --unit=sshd.service -n 20 --no-pager

vi /home/bob/ip.txt
# Identify the PID of the process named rpcbind and save its value in /home/bob/pid.txt file.

pgrep -a rpcbind
# With the systemctl command, find out the PID of the process currently managed by the sshd.service. Send the SIGHUP signal to this process.
systemctl status sshd.service
sudo kill -SIGHUP <pid>

# Assign nice value 15 to bash process ran by user bob.

nice -n 15 bash


# Analiyze the error logs through journalctl with the priority flag and copy the output to /home/bob/.priority/priority.log
sudo journalctl -p err > .priority/priority.log
# Analyse the info priority logs through journalctl that begin with letter c and store the output in /home/bob/.priority/boot.log file.

sudo journalctl -p info -g '^c' 

# Run a command to sleep for 3000 seconds and make sure its running in the background.

sleep 3000 &

