# Manual Enum (CMD)

### 1. System Enumeration:

#### System Info:

```batch
systeminfo | findstr /B /C:"OS Name" /C:"OS Version" /C:"System Type"
```

#### Installed Patch:

```batch
wmic qfe
```

* Filtered Version

```batch
wmic qfe get Caption,Description,HotFixID,InstalledOn
```

#### LocalDisk Info:

```batch
wmic localdisk get caption
```

###

### 2. User Enumeration:

#### User Info:

```batch
whoami
```

#### User Privilege:

```batch
whoami /priv
```

#### Group Info:

```batch
whoami /groups
```

#### User Accounts

```batch
net user
```

#### User Info:

```batch
net user <USER_NAME>
```

#### Group Info:

```batch
net localgroup
```

* For a specific know group name.

```batch
net localgroup <GROUP_NAME>
```

###

### 3. Network Enumeration:

#### ARP Table:

```batch
arp -a
```

#### Routing Table:

```batch
route print
```

#### Listening Ports:

```batch
netstat -ano
```

###

### 4. Antivirus and Firewall Enumeration:

```batch
#Using the Windows Sevice Control
sc query windefend

#We can also list all services running using the sc
sc queryex type= service

#For firewall information
netsh advfirewall firewall dump
             OR
netsh firewall show state

#For firewall configurations
netsh firewall show config

```
