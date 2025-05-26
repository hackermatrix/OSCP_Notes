# Manual Enum

#### User and Group Information

* **Check current user context**:\
  `id`
* **List all users**:\
  `cat /etc/passwd`
* **View shadow file (requires root)**:\
  `cat /etc/shadow`

#### System Information

* **Get hostname**:\
  `hostname`
* **Check OS version and kernel**:\
  `cat /etc/issue`\
  `cat /etc/os-release`\
  `uname -a`\
  (Kernel version, architecture, and distribution details)

#### Process Enumeration

* **List all running processes**:\
  `ps aux`\
  (Shows processes, owners, and resource usage)
* **Filter processes by user**:\
  `ps aux | grep <username>`

#### Network Configuration

* **List network interfaces**:\
  `ip a` or `ifconfig -a`
* **View routing table**:\
  `routel` or `route -n`
* **Check active connections/listening ports**:\
  `ss -anp` or `netstat -tulnp`

#### Firewall Rules

* **Check iptables rules (requires root)**:\
  `iptables -L`
* **Read saved firewall rules (if permissions allow)**:\
  `cat /etc/iptables/rules.v4`

#### Scheduled Tasks (Cron Jobs)

* **List system-wide cron jobs**:\
  `ls -lah /etc/cron*`\
  `cat /etc/crontab`
* **Check current user's cron jobs**:\
  `crontab -l`
* **Check root's cron jobs (if sudo allows)**:\
  `sudo crontab -l`

#### Installed Software

* **List installed packages (Debian)**:\
  `dpkg -l`
* **List installed packages (Red Hat)**:\
  `rpm -qa`

#### File Permission Checks

* **Find world-writable files**:\
  `find / -type f -perm -o=w 2>/dev/null`
* **Find SUID/SGID files**:\
  `find / -type f -perm -u=s -o -perm -g=s 2>/dev/null`
* **Find files owned by root but writable by current user**:\
  `find / -type f -user root -writable 2>/dev/null`

#### Additional Useful Commands

* **Check sudo privileges**:\
  `sudo -l`\
  (Lists allowed commands for the current user)
* **Search for sensitive files (e.g., passwords)**:\
  `grep -r "password" /etc/ 2>/dev/null`\
  `find / -name "*.conf" -type f 2>/dev/null`
