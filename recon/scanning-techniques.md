---
description: Useful nmap scanning Techniques
---

# Scanning Techniques

### Ping Sweep

```markdown
nmap -sP 192.168.1.0/24 -oN scan-alive-hosts.txt
nmap -sP 192.168.1.1,5,100,150 -oN scan-alive-hosts.txt
```

### General Scans for a Host

```markdown
Default script, All ports, Version + OS Discovery, TCP scan
nmap -sC -A -T4 -oN nmap-tcp-initial.txt 192.168.1.1 -p-
```

### UDP Scan

```markdown
nmap -sU --top-ports 100 -oN nmap-udp-initial.txt 192.168.1.1
```

### Scan a Single Target

```markdown
nmap [target]
```

### Scan Multiple Targets

```markdown
nmap [target1, target2, etc]
```

### Scan a List of Targets

```markdown
nmap -iL [list.txt]
```

### Scan a Range of Hosts

```markdown
nmap [range of IP addresses]
```

### Scan an Entire Subnet

```markdown
nmap [ip address/cdir]
```

### Scan Random Hosts

```markdown
nmap -iR [number]
```

### Exclude Targets From a Scan

```markdown
nmap [targets] --exclude [targets]
```

### Exclude Targets Using a List

```markdown
nmap [targets] --excludefile [list.txt]
```

### Perform an Aggressive Scan

```bash
nmap -A [target]
```

### Scan an IPv6 Target

```markdown
nmap -6 [target]
```

## A. Port Scanning Options

#### Perform a Fast Scan

```markdown
nmap -F [target]
```

#### Scan Specific Ports

```markdown
nmap -p [port(s)] [target]
```

#### Scan Ports by Name

```markdown
nmap -p [port name(s)] [target]
```

#### Scan Ports by Protocol

```markdown
nmap -sU -sT -p U:[ports],T:[ports] [target]
```

#### Scan All Ports

```markdown
nmap -p 1-65535 [target]
```

#### Scan Top Ports

```markdown
nmap --top-ports [number] [target]
```

#### Perform a Sequential Port Scan

```markdown
nmap -r [target]
```

#### Attempt to Guess an Unknown OS

```markdown
nmap -O --osscan-guess [target]
```

### Service Version Detection

```markdown
nmap -sV [target]
```

### Troubleshoot Version Scan

```markdown
nmap -sV --version-trace [target]
```

### Perform an RPC Scan

```markdown
nmap -sR [target]
```

## B. Discovery Options

#### Host Discovery

The -p switch determines the type of ping to perform.

```markdown
Nmap Switch Description
-PI ICMP ping
-Po No ping
-PS SYN ping
-PT TCP ping
```

#### Perform a Ping Only Scan

```markdown
nmap -sn [target]
```

#### Do Not Ping

```markdown
nmap -Pn [target]
```

#### TCP SYN Ping

```markdown
nmap -PS [target]
```

#### TCP ACK Ping

```markdown
nmap -PA [target]
```

#### UDP Ping

```markdown
nmap -PU [target]
```

#### SCTP INIT Ping

```markdown
nmap -PY [target]
```

#### ICMP Echo Ping

```markdown
nmap -PE [target]
```

#### ICMP Timestamp Ping

```markdown
nmap -PP [target]
```

#### ICMP Address Mask Ping

```markdown
nmap -PM [target]
```

#### IP Protocol Ping

```markdown
nmap -PO [target]
```

#### ARP Ping

```markdown
nmap -PR [target]
```

#### Traceroute

```markdown
nmap --traceroute [target]
```

#### Force Reverse DNS Resolution

```markdown
nmap -R [target]
```

#### Disable Reverse DNS Resolution

```markdown
nmap -n [target]
```

#### Alternative DNS Lookup

```markdown
nmap --system-dns [target]
```

#### Manually Specify DNS Server

Can specify a single server or multiple.

```markdown
nmap --dns-servers [servers] [target]
```

#### Create a Host List

```markdown
nmap -sL [targets]
```

### Port Specification and Scan Order

```markdown
Nmap Switch Description
```

### Service/Version Detection

```markdown
Nmap Switch Description
-sV Enumerates software versions
```

### Script Scan

```markdown
Nmap Switch Description
-sC Run all default scripts
```

### OS Detection

```markdown
Nmap Switch Description
```

### Timing and Performance

The -t switch determines the speed and stealth performed.

```markdown
Nmap Switch Description
-T0 Serial, slowest scan
-T1 Serial, slow scan
-T2 Serial, normal speed scan
-T3 Parallel, normal speed scan
-T4 Parallel, fast scan
```

Not specifying a T value will default to -T3, or normal speed.

## C. Firewall Evasion Techniques

```markdown
Nmap Switch Description
```

### Firewall/IDS Evasion and Spoofing

#### Fragment Packets

```markdown
nmap -f [target]
```

#### Specify a Specific MTU

```markdown
nmap --mtu [MTU] [target]
```

#### Use a Decoy

```markdown
nmap -D RND:[number] [target]
```

#### Idle Zombie Scan

```markdown
nmap -sI [zombie] [target]
```

#### Manually Specify a Source Port

```markdown
nmap --source-port [port] [target]
```

#### Append Random Data

```markdown
nmap --data-length [size] [target]
```

#### Randomize Target Scan Order

```markdown
nmap --randomize-hosts [target]
```

#### Spoof MAC Address

```markdown
nmap --spoof-mac [MAC|0|vendor] [target]
```

#### Send Bad Checksums

```markdown
nmap --badsum [target]
```

## D. Advanced Scanning Functions

#### TCP SYN Scan

```markdown
nmap -sS [target]
```

#### TCP Connect Scan

```markdown
nmap -sT [target]
```

#### UDP Scan

```markdown
nmap -sU [target]
```

#### TCP NULL Scan

```markdown
nmap -sN [target]
```

#### TCP FIN Scan

```markdown
nmap -sF [target]
```

#### Xmas Scan

```markdown
nmap -sA [target]
```

#### TCP ACK Scan

```markdown
nmap -sA [target]
```

#### Custom TCP Scan

```markdown
nmap --scanflags [flags] [target]
```

#### IP Protocol Scan

```markdown
nmap -

sO [target]
```

#### Send Raw Ethernet Packets

```markdown
nmap --send-eth [target]
```

#### Send IP Packets

```markdown
nmap --send-ip [target]
```

## E. Timing Options

#### Timing Templates

```markdown
nmap -T[0-5] [target]
```

#### Set the Packet TTL

```markdown
nmap --ttl [time] [target]
```

#### Minimum Number of Parallel Operations

```markdown
nmap --min-parallelism [number] [target]
```

#### Maximum Number of Parallel Operations

```markdown
nmap --max-parallelism [number] [target]
```

#### Minimum Host Group Size

```markdown
nmap --min-hostgroup [number] [targets]
```

#### Maximum Host Group Size

```markdown
nmap --max-hostgroup [number] [targets]
```

#### Maximum RTT Timeout

```markdown
nmap --initial-rtt-timeout [time] [target]
```

#### Initial RTT Timeout

```markdown
nmap --max-rtt-timeout [TTL] [target]
```

#### Maximum Number of Retries

```markdown
nmap --max-retries [number] [target]
```

#### Host Timeout

```markdown
nmap --host-timeout [time] [target]
```

#### Minimum Scan Delay

```markdown
nmap --scan-delay [time] [target]
```

#### Maximum Scan Delay

```markdown
nmap --max-scan-delay [time] [target]
```

#### Minimum Packet Rate

```markdown
nmap --min-rate [number] [target]
```

#### Maximum Packet Rate

```markdown
nmap --max-rate [number] [target]
```

#### Defeat Reset Rate Limits

```markdown
nmap --defeat-rst-ratelimit [target]
```
