## What is Mark's password?

For this sections exercise, imagine that we compromised the password hash of a **work email** belonging to **Mark White**. After performing a bit of OSINT, we have gathered the following information about Mark:

* He was born on **August 5, 1998**
* He works at **Nexura, Ltd**.
  - The company's password policy requires passwords to be at least 12 characters long, to contain at least one uppercase letter, at least one lowercase letter, at least one symbol and at least one number
* He lives in **San Francisco, CA, USA**
* He has a pet cat named **Bella**
* He has a wife named **Maria**
* He has a son named **Alex**
* He is a big fan of **baseball**

The password hash is: **97268a8ae45ac7d15c3cea4ce6ea550b**. Use the techniques covered in this section to generate a custom wordlist and ruleset targeting Mark specifically, and crack the password.


```
nano mark.html

<html>
<body>
<h1>Mark White</h1>
<ul>
<li>born: August 5, 1998</li>
<li>works: Nexura, Ltd</li>
<li>lives: San Francisco, CA, USA</li>
<li>pet: Bella</li>
<li>wife: Maria</li>
<li>son: Alex</li>
<li>fan: baseball</li>
</ul>
</body>
</html>
```

```
python3 -m http.server 8080
cewl http://<tun0>:8000/mark.html -d 4 -m 6 --lowercase -w mark.txt

hashcat --stdout -a 1 mark.txt mark.txt > mark_pairs.txt

awk 'length($0) >= 12' mark_pairs.txt > pairs_length12.txt 
```

```
nano custom.rule

:
c
so0
c so0
sa@
c sa@
c sa@ so0
$!
$! c
$! so0
$! sa@
$! c so0
$! c sa@
$! so0 sa@
$! c so0 sa@
```

```
hashcat --stdout -r custom.rule pairs_length12.txt > mark_password.list
hashcat --force mark.txt -r custom.rule --stdout | sort -u > mark_password.list
hashcat -a 0 -m 0 97268a8ae45ac7d15c3cea4ce6ea550b mark_password.list
```