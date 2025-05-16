---
icon: plug
---

# Manual Enum (PowerShell)

```powershell
# 1. Gets the list of all the Local Users
Get-LocalUser

# 2. Gets the list of all the Local Groups
Get-LocalGroup

# 3. Get all the group member names in this group
Get-LocalGroupMember <_Group_Name_>

# 4. Get operating system, version, and architecture
systeaminfo

# 5. Get all network interfaces
ipconfig /all

# 6. Get the Routing Table of the system
route print

# 7. Get all the TCP and UDP active connections with the Process ID (PIDs)
netstat -ano

# 8. Get Installed Applications 

#32 bit:
Get-ItemProperty "HKLM:\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Uninstall\*" | select displayname  
#64 bit:
Get-ItemProperty "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall\*" | select displayname 

# 9. Get Running Processes:
Get-Process

# 10. Get User's Command Execution History:
Get-History 

# 11. PSReadLine :(It stores the Command Execution History even accross sessions and this History is not cleared even if we use 'Clear-History'
# Get its Content:
cat (Get-PSReadlineOption).HistorySavePath

# 12. Get Running Services (May give permission denined when used in WinRM or PS-Session shell but works with RDP )
Get-CimInstance -ClassName win32_service | Select State | Where-object {$_.State -like 'Running'}
 
# 13. Get the Permissions on a given file :
icacls <path_fo_the_file>

# 14.
```
