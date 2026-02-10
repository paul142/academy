## Use the credentials provided to log into the target machine and retrieve the MySQL credentials. Submit them as the answer. (Format: <username>:<password>)
```
pipx install defaultcreds-cheat-sheet
creds search mysql

ssh sam@10.129.202.64 
mysql -u superdba -p
admin
```