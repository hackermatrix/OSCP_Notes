# Windows enum (CMD)

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

