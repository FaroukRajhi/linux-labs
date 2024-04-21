# By default UFW (Uncomplicated Firewall) is disabled. So before proceeding into the lab,

Turn on UFW
All traffic is blocked by default, so we must allow SSH on port 22 so the lab won't be broken.

Start ufw with

sudo ufw enable
All traffic is blocked by default, so we must allow SSH on port 22 so the lab won't be broken.

sudo ufw allow 22

# Set up a firewall rule to allow incoming traffic to this machine on port 80.

sudo ufw allow 80

# Set up a firewall rule to allow incoming traffic to this machine on port 53, through the TCP protocol.

sudo ufw allow 53/tcp

# Set up a firewall rule to deny incoming traffic to this machine on port 443, through the TCP protocol.

sudo ufw deny 443/tcp

# Delete a firewall rule denying incoming traffic to this machine on port 443, through the TCP protocol (That is created in previous step).

sudo ufw delete deny 443/tcp

# Allow all traffic that is coming from the following IP address 207.45.232.181.

sudo ufw allow from 207.45.232.181

# Allow all traffic that is coming from any IP in this network range: 10.11.12.0 to 10.11.12.255 (i.e 10.11.12.0/24), add the required rule.

sudo ufw allow from 10.11.12.0/24 

# There's a firewall rule that denies any traffic coming from the 10.0.0.19 IP address. But this rule is in an incorrect spot (after an allow rule for the 10.0.0.0/24 range). So traffic is never denied because the rule is never matched. Correct this mistake.

First check for number of rule

~ ➜  sudo ufw status numbered
Status: active

     To                         Action      From
     --                         ------      ----
[ 1] 22/tcp                     ALLOW IN    192.168.0.0/24            
[ 2] 22                         ALLOW IN    192.168.0.4               
[ 3] 22                         ALLOW IN    Anywhere                  
[ 4] 80                         ALLOW IN    Anywhere                  
[ 5] 53/tcp                     ALLOW IN    Anywhere                  
[ 6] Anywhere                   ALLOW IN    207.45.232.181            
[ 7] Anywhere                   ALLOW IN    10.11.12.0/24             
[ 8] 3306                       ALLOW IN    10.0.0.0/24               
[ 9] 22 (v6)                    ALLOW IN    Anywhere (v6)             
[10] 80 (v6)                    ALLOW IN    Anywhere (v6)             
[11] 53/tcp (v6)                ALLOW IN    Anywhere (v6)             
Delete the rule as per requirement

~ ➜  sudo ufw delete 8
Deleting:
 allow from 10.0.0.0/24 to any port 3306
Proceed with operation (y|n)? y
Rule deleted
Insert rule using the below command

~ ➜ sudo ufw insert 1 deny from 10.0.0.19
Rule inserted
Check status again

~ ➜ sudo ufw status numbered

