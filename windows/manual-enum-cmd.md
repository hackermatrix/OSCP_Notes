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

