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
