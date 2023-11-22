# 161 - SNMP

*   **Management Information Base (MIB)** :&#x20;

    MIB is an **independent format for storing device information**. A MIB is a **text** file in which all queryable **SNMP objects** of a device are listed in a **standardized** tree hierarchy. It contains at **least one `Object Identifier` (`OID`).**



*   **`Object Identifier` (`OID`):**

    OIDs uniquely identify managed objects in a MIB hierarchy

## 1. SNMPwalk

SNMPwalk is a great tool to query MIB values to retrieve information about managed devices, but, as a minimum, **it requires a valid SNMP read-only community string.**

```
for community in public private manager; do snmpwalk -c $community -v1 $ip; done
# here it will take three comunity strings and check one by one

snmpwalk -c public -v1 $ip

snmpwalk -c public -v2c <target-ip>
# here -c stands for community string and 2c is most common version found on today's snmp devices
```

## 2. SNMPcheck

Same as `snmpwalk` but give nice output

```
snmpcheck -t 192.168.1.X -c public
```

## 3. Brute forcing community string

### OneSixtyOne

* Onesixtyone is a very fast tool to brute force SNMP community strings and take advantage of the connectionless protocol. Onesixtyone sends an SNMP request and (by default) waits 10 milliseconds for a response. If the community string sent by onesixtyone to the SNMP enabled device is invalid, then the request is dropped. However, if a valid community string is passed to an SNMP enabled device, the device responds with the information requested (the ‘system.sysDescr.0’ value).

```
onesixtyone -c dict.txt <ip>
```

## Wordlists&#x20;

```
/usr/share/seclists/Discovery/SNMP/common-snmp-community-strings-onesixtyone.txt

/usr/share/metasploit-framework/data/wordlists/snmp_default_pass.txt
```

## 4. NSE Script

```
ls -l /usr/share/nmap/scripts/snmp*
```

## 5. SNMPv3 Enumeration

```
wget https://raw.githubusercontent.com/raesene/TestingScripts/master/snmpv3enum.rb; ./snmpv3e
```

#### References:

{% embed url="https://book.hacktricks.xyz/network-services-pentesting/pentesting-snmp" %}
SNMP versions
{% endembed %}

{% embed url="https://gabb4r.gitbook.io/oscp-notes/service-enumeration/snmp-enumeraion" %}
Read About Community Strings
{% endembed %}

