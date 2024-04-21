Also called port forwarding.
We can create rules that tell our public server where to redirect incoming connections  to a variety of different ports.
For example, you know for connections for port 80, port 993, and port 3306.
In this case, anything incoming on port 80, we can redirect or forward to server 1 and so on.

# Set up port forwarding in linux
enable ip forwarding
/etc/sysctl.conf ot /etc/sysctl.d/99-sysctl.conf
uncomment net.ipv4_forward=1
To save changes
sysctl --system

All handled by linux kernel

netfiler (iptables)

example:
We want to redirect every request coming from 10.0.0.0/24 to port 8080 on an a machine should be redirected to port 80 on a remote server with an IP address of 192.168.0.5.
First we will see what network interfaces will be responsible for this redirection.
Let's assume that there are two network interfaces: one deals with the incoming traffic from 10.0.0.0/24 and the other one deals with the outgoing traffic to 192.168.0.5 which sits on different network.
check route table.

**iptables parameters**

- -t nat: to add this rule to the "nat" table. Since when a port is redirected, NAT is used, to change the initial destination IP and port, to a different IP and Port.
  So whenever we need NAT, we add our rule to the nat table.
- With -A PREROUTING we append another rule to the "PREROUTING" chain which deals with altering network packets as soon as they received.
- With -i eth0 we select eth0 as the input interface. This way, we only apply this rule when the packet is received on a specific interface.
- With the -s option we pick the source IP. So we apply this rule only the source IP matches anything in the 10.0.0.0/24.
Another way to say it is that we only redirect this packet