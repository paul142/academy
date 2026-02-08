## Download the attached ZIP file (linux-authentication-process.zip), and use single crack mode to find martin's password. What is it?

```
wget https://academy.hackthebox.com/storage/modules/147/linux-authentication-process.zip
unzip linux-authentication-process.zip
unshadow passwd shadow > unshadowed.hashes
hashcat -m 1800 -a 0 unshadowed.hashes /usr/share/wordlists/rockyou.txt -o unshadowed.cracked
john --single unshadowed.hashes
```


## Use a wordlist attack to find sarah's password. What is it?
```
unshadow passwd shadow| tee unshadowed.hashes
echo '$6$EBOM5vJAV1TPvrdP$LqsLyYkoGzAGt4ihyvfhvBrrGpVjV976B3dEubi9i95P5cDx1U6BrE9G020PWuaeI6JSNaIDIbn43uskRDG0U/' | tee sarah
hashcat -a 0 -m 1800 sarah /usr/share/wordlists/rockyou.txt --show
```