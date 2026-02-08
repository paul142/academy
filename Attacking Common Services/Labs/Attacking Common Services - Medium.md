# Attacking Common Services - Medium

The second server is an internal server (within the inlanefreight.htb domain) that manages and stores emails and files and serves as a backup of some of the company's processes. From internal conversations, we heard that this is used relatively rarely and, in most cases, has only been used for testing purposes so far.

## Assess the target server and find the flag.txt file. Submit the contents of this file as your answer.

```
nmap -p- -sV -A 10.129.201.127
ftp 10.129.201.127 30021
     anonymous
cd simon
get mynotes.txt

ftp simon@10.129.201.127 30021
p: 8Ns8j1b!23hs4921smHzwn

```
