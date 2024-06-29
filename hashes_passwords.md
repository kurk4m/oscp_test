JOHN:
zip2john backup.zip > hashes
john -wordlist=/usr/share/wordlists/rockyou.txt hashes
gzip -d /usr/share/wordlists/rockyou.txt.gz 
john --show hashes

hashid 2cb42f8734ea607eefed3b70af13bbd3
