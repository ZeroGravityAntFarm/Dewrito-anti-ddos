# Eldewrito Anti DDOS
Some hardening tips for your eldewrito server (Linux only).


### Limit the number of connections from a single address on the game ports
```bash
for i in {11774...11777}; do 
    iptables -A INPUT -p tcp --syn --dport $i -m connlimit --connlimit-above 3 -j DROP;
done
```




### Mass block known malicious ip addresses and ranges using a firehole netset (works with any ip list). Firehol level1 can be found here: https://github.com/firehol/blocklist-ipsets/blob/master/firehol_level1.netset
```bash
#!/bin/bash
filename='firehol_level1.netset'

while read p; do
    ip route add blackhole $p
done < $filename
```




### Remove the ip block list
```bash
#!/bin/bash
filename='firehol_level1.netset'

while read p; do
    ip route del $p
done < $filename
```




### Enable Syn Cookies
```bash
vim /etc/sysctl.conf

Add the following line:
net.ipv4.tcp_syncookies = 1

Reload with:
sysctl -p
```




### Protect ssh with fail2ban
```bash
apt-get install fail2ban
```




### Disable ssh root login
```bash
vim /etc/ssh/sshd_config

Add:
PermitRootLogin no

Restart sshd:
sudo service ssh restart
```
