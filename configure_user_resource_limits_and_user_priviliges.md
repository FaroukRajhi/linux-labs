# Add an environment variable for user bob.


The variable name should be MYVAR and its value should be TRUE

vi ~/.bashrc
export MYVAR=TRUE
save the file and run:

source ~/.bashrc

# Whenever we add a new user to the system, some files are copied, from a template directory to the user's home directory.

sudo cp /etc/skel/.bash* /home/bob/default_data/

# Make sure that this command gets executed for any user that logs in to the system:
echo Welcome to our server!

sudo vi /etc/profile.d/welcome.sh



and save below given line in it:


echo "Welcome to our server!"

# Make sure that every time a new user account is added to the system, a file called README is copied to the new user's home directory.

sudo touch /etc/skel/README

# Set a variable named LFCS with value Welcome to the KodeKloud LFCS Labs! for every user that logs into this system.

sudo vi /etc/environment
LFCS=Welcome to the KodeKloud LFCS Labs!

# Update the value of $PATH variable for user bob to include $HOME/.config/bin location in the path.

vi /home/bob/.bashrc
PATH="$HOME/.local/bin:$HOME/bin:$HOME/.config/bin:$PATH"
source ~/.bashrc