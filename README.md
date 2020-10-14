# dewrito-anti-ddos
Some hardening tips for your eldewrito server.


```bash
for i in {11774...11777}; do 
    iptables -A INPUT -p tcp --syn --dport $i -m connlimit --connlimit-above 3 -j DROP;
done
```
