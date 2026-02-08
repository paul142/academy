## Find all available DNS records for the "inlanefreight.htb" domain on the target name server and submit the flag found as a DNS record as the answer.
```
nmap -p53 -Pn -sV -sC 10.129.203.6

nano /etc/hosts
10.129.203.6    inlanefreight.htb

git clone https://github.com/TheRook/subbrute.git >> /dev/null 2>&1
cd subbrute

echo "10.129.203.6" > resolvers.txt
python3 subbrute.py -p inlanefreight.htb -s names.txt -r resolvers.txt

dig AXFR hr.inlanefreight.htb @10.129.203.6


```

