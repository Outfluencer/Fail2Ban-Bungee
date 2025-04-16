# Fail2Ban-Bungee
Blocks connections that are causing exceptions in initial connection state

# Setup
```
sudo apt install iptables
sudo apt install ipset
sudo apt install fail2ban
```

`nano /etc/fail2ban/jail.conf`
Append this at the bottom
```
[bungeecord-initial]
enabled = true
filter = bungeecord-initial
logpath = /home/bungee/proxy.log.0
maxretry = 1
findtime = 60
bantime = 300
banaction = iptables-ipset-proto4
port = 25577
backend = auto
```

`nano /etc/fail2ban/filter.d/bungeecord-initial.conf`
Add this to the file

```
[Definition]
failregex =\/<HOST>:\d+\] <-> InitialHandler -
ignoreregex =executed command:
```

`systemctl restart fail2ban`
