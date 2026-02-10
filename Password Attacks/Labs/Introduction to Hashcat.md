## Use a dictionary attack to crack the first password hash. (Hash: e3e3ec5831ad5e7288241960e5d4fdb8)
```
hashcat -a 0 -m 0 e3e3ec5831ad5e7288241960e5d4fdb8 /usr/share/wordlists/rockyou.txt

hashcat -m 0 --show e3e3ec5831ad5e7288241960e5d4fdb8
```

## Use a dictionary attack with rules to crack the second password hash. (Hash: 1b0556a75770563578569ae21392630c)
```
hashcat -a 0 -m 0 1b0556a75770563578569ae21392630c /usr/share/wordlists/rockyou.txt -r /usr/share/hashcat/rules/best66.rule

hashcat -m 0 --show 1b0556a75770563578569ae21392630c
```

## Use a mask attack to crack the third password hash. (Hash: 1e293d6912d074c0fd15844d803400dd)
```
hashcat -a 3 -m 0 1e293d6912d074c0fd15844d803400dd '?u?l?l?l?l?d?s'

hashcat -m 0 --show 1e293d6912d074c0fd15844d803400dd
```
