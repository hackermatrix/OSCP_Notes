---
icon: lightbulb-exclamation-on
---

# Windows Fundamentals

### Windows Services:

* Services are a major component of the Windows operating system. They allow for the creation and management of long-running processes. Windows services can be started automatically at system boot without user intervention. These services can continue to run in the background even after the user logs out of their account on the system.
* Windows Services are managed by **SCM** (Service Control Manager).
*



#### &#x20;Critical windows services:

| Service                   | Description                                                                                                                                                                                                                                             |
| ------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| smss.exe                  | Session Manager SubSystem. Responsible for handling sessions on the system.                                                                                                                                                                             |
| csrss.exe                 | Client Server Runtime Process. The user-mode portion of the Windows subsystem.                                                                                                                                                                          |
| wininit.exe               | Starts the Wininit file .ini file that lists all of the changes to be made to Windows when the computer is restarted after installing a program.                                                                                                        |
| logonui.exe               | Used for facilitating user login into a PC                                                                                                                                                                                                              |
| lsass.exe                 | The Local Security Authentication Server verifies the validity of user logons to a PC or server. It generates the process responsible for authenticating users for the Winlogon service.                                                                |
| services.exe              | Manages the operation of starting and stopping services.                                                                                                                                                                                                |
| winlogon.exe              | Responsible for handling the secure attention sequence, loading a user profile on logon, and locking the computer when a screensaver is running.                                                                                                        |
| System                    | A background system process that runs the Windows kernel.                                                                                                                                                                                               |
| svchost.exe with RPCSS    | Manages system services that run from dynamic-link libraries (files with the extension .dll) such as "Automatic Updates," "Windows Firewall," and "Plug and Play." Uses the Remote Procedure Call (RPC) Service (RPCSS).                                |
| svchost.exe with Dcom/PnP | Manages system services that run from dynamic-link libraries (files with the extension .dll) such as "Automatic Updates," "Windows Firewall," and "Plug and Play." Uses the Distributed Component Object Model (DCOM) and Plug and Play (PnP) services. |



#### Local Security Authority Subsystem Service (LSASS)

`lsass.exe` is the process that is responsible for enforcing the security policy on Windows systems. When a user attempts to log on to the system, this process verifies their log on attempt and creates access tokens based on the user's permission levels. LSASS is also responsible for user account password changes. All events associated with this process (logon/logoff attempts, etc.) are logged within the Windows Security Log. LSASS is an extremely high-value target as several tools exist to extract both cleartext and hashed credentials stored in memory by this process.



***



### Windows Sessions:

* There are two types of windows logon sessions:
  * Interactive&#x20;
  * Non-Interactive

#### Interactive Sessions:

* Initiated by a user authenticating to a local or domain system by entering their credentials

**Non-Interactive:**

* Do not require login credentials.
* Generally used by the Windows operating system to automatically start services and applications without requiring user interaction.
* There are three types of Non-Interactive accounts.

| Account                 | Description                                                                                                                                                                                                                                                            |
| ----------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Local System Account    | Also known as the `NT AUTHORITY\SYSTEM` account, this is the most powerful account in Windows systems. It is used for a variety of OS-related tasks, such as starting Windows services. This account is more powerful than accounts in the local administrators group. |
| Local Service Account   | Known as the `NT AUTHORITY\LocalService` account, this is a less privileged version of the SYSTEM account and has similar privileges to a local user account. It is granted limited functionality and can start some services.                                         |
| Network Service Account | This is known as the `NT AUTHORITY\NetworkService` account and is similar to a standard domain user account. It has similar privileges to the Local Service Account on the local machine. It can establish authenticated sessions for certain network services.        |

***

## Windows Management Instrumentation (WMI)

* **WMI** is a subsystem of PowerShell that provides system administrators with powerful tools for system monitoring.
* Some of the uses for WMI are:
  * Status information for local/remote systems
  * Configuring security settings on remote machines/applications
  * Setting and changing user and group permissions
  * Setting/modifying system properties
  * Code execution
  * Scheduling processes
  * Setting up logging

***

### Microsoft Management Console (MMC)

* The MMC can be used to group snap-ins, or administrative tools, to manage hardware, software, and network components within a Windows host.

***

### Windows Security

#### Security Accounts Manager (SAM) and Access Control Entries (ACE):

* **SAM**: SAM grants rights to a network to execute specific processes.
* **ACE:**The access rights themselves are managed by Access Control Entries (ACE) in Access Control Lists (ACL). The ACLs contain ACEs that define which users, groups, or processes have access to a file or to execute a process, for example.
* The permissions to access a securable object are given by the security descriptor, classified into two types of ACLs: the `Discretionary Access Control List (DACL)` or `System Access Control List (SACL)`. Every thread and process started or initiated by a user goes through an authorization process. An integral part of this process is access tokens, validated by the Local Security Authority (LSA). In addition to the SID, these access tokens contain other security-relevant information.

***

### User Account Control (UAC)

* A security feature in Windows to prevent malware from running or manipulating processes that could damage the computer or its contents.
*

