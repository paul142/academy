## Run the above target then navigate to http://ip:port/download, then extract the downloaded file. Inside, you will find a password-protected VHD file. Crack the password for the VHD and submit the recovered password as your answer.
```
/usr/sbin/bitlocker2john -i Private.vhd > Private.hashes
grep "bitlocker\$0" Private.hashes > Private.hash
cat Private.hash

hashcat -m 22100 -a 0 '$bitlocker$0$16$b3c105c7ab7faaf544e84d712810da65$1048576$12$b020fe18bbb1db0103000000$60$e9c6b548788aeff190e517b0d85ada5daad7a0a3f40c4467307011ac17f79f8c99768419903025fd7072ee78b15a729afcf54b8c2e3af05bb18d4ba0' /usr/share/wordlists/rockyou.txt

```

## Mount the BitLocker-encrypted VHD and enter the contents of flag.txt as your answer.
```
sudo apt-get install dislocker
sudo mkdir -p /media/bitlocker
sudo mkdir -p /media/bitlockermount

sudo losetup -f -P Private.vhd
sudo losetup -d /dev/loop0

sudo dislocker -V /dev/loop0p1 -u"francisco" -- /media/bitlocker
sudo mount -o loop /media/bitlocker/dislocker-file /media/bitlockermount
cd /media/bitlockermount
cat flag.txt

```
