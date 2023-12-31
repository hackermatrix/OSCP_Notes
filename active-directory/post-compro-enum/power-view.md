# Power View

1. **Basic Enumeration**

<pre class="language-powershell"><code class="lang-powershell"><strong>#Basic Domain Information
</strong>Get-NetDomain

<strong>#User Information
</strong>Get-NetUser
Get-NetUser | select samaccountname, description, logoncount
Get-NetUser -UACFilter NOT_ACCOUNTDISABLE | select samaccountname, description, pwdlastset, logoncount, badpwdcount
Get-NetUser -LDAPFilter '(sidHistory=*)'
Get-NetUser -PreauthNotRequired
Get-NetUser -SPN

<strong>#Groups Information
</strong>Get-NetGroup | select samaccountname,description
Get-DomainObjectAcl -SearchBase 'CN=AdminSDHolder,CN=System,DC=EGOTISTICAL-BANK,DC=local' | %{ $_.SecurityIdentifier } | Convert-SidToName

<strong>#Computers Information
</strong>Get-NetComputer | select samaccountname, operatingsystem
Get-NetComputer -Unconstrained | select samaccountname 
Get-NetComputer -TrustedToAuth | select samaccountname
Get-DomainGroup -AdminCount | Get-DomainGroupMember -Recurse | ?{$_.MemberName -like '*

<strong># Domain Information
</strong><strong>
</strong>Get-NetDomain #Get info about the current domain
Get-NetDomain -Domain mydomain.local
Get-DomainSID #Get domain SID
​
# Policy
Get-DomainPolicy #Get info about the policy
(Get-DomainPolicy)."KerberosPolicy" #Kerberos tickets info(MaxServiceAge)
(Get-DomainPolicy)."System Access" #Password policy
(Get-DomainPolicy).PrivilegeRights #Check your privileges
​
# Domain Controller
Get-NetDomainController -Domain mydomain.local #Get Domain Controller

</code></pre>



#### 2. Users, Groups and Computers

<pre class="language-powershell"><code class="lang-powershell"><strong># Users
</strong>Get-NetUser #Get users with several (not all) properties
Get-NetUser | select -ExpandProperty samaccountname #List all usernames
Get-NetUser -UserName student107 #Get info about a user
Get-NetUser -properties name, description #Get all descriptions
Get-NetUser -properties name, pwdlastset, logoncount, badpwdcount #Get all pwdlastset, logoncount and badpwdcount
Find-UserField -SearchField Description -SearchTerm "built" #Search account with "something" in a parameter
​
<strong># Users Filters
</strong>Get-NetUser -UACFilter NOT_ACCOUNTDISABLE -properties distinguishedname #All enabled users
Get-NetUser -UACFilter ACCOUNTDISABLE #All disabled users
Get-NetUser -UACFilter SMARTCARD_REQUIRED #Users that require a smart card
Get-NetUser -UACFilter NOT_SMARTCARD_REQUIRED -Properties samaccountname #Not smart card users
Get-NetUser -LDAPFilter '(sidHistory=*)' #Find users with sidHistory set
Get-NetUser -PreauthNotRequired #ASREPRoastable users
Get-NetUser -SPN | select serviceprincipalname #Kerberoastable users
Get-NetUser -SPN | ?{$_.memberof -match 'Domain Admins'} #Domain admins kerberostable
Get-Netuser -TrustedToAuth #Useful for Kerberos constrain delegation
Get-NetUser -AllowDelegation -AdminCount #All privileged users that aren't marked as sensitive/not for delegation

<strong>#Groups
</strong>Get-NetGroup #Get groups
Get-NetGroup -Domain mydomain.local #Get groups of an specific domain
Get-NetGroup 'Domain Admins' #Get all data of a group
Get-NetGroup -AdminCount #Search admin grups
Get-NetGroup -UserName "myusername" #Get groups of a user
Get-NetGroupMember -Identity "Administrators" -Recurse #Get users inside "Administrators" group. If there are groups inside of this grup, the -Recurse option will print the users inside the others groups also
Get-NetGroupMember -Identity "Enterprise Admins" -Domain mydomain.local #Remember that "Enterprise Admins" group only exists in the rootdomain of the forest
Get-NetLocalGroup -ComputerName dc.mydomain.local -ListGroups #Get Local groups of a machine (you need admin rights in no DC hosts)
Get-NetLocalGroupMember -computername dcorp-dc.dollarcorp.moneycorp.local #Get users of localgroups in computer
Get-DomainObjectAcl -SearchBase 'CN=AdminSDHolder,CN=System,DC=testlab,DC=local' -ResolveGUIDs #Check AdminSDHolder users
Get-NetGPOGroup #Get restricted groups
​
<strong># Computers
</strong>Get-NetComputer #Get all computer objects
Get-NetComputer -Ping #Send a ping to check if the computers are working
Get-NetComputer -Unconstrained #DCs always appear but aren't useful for privesc
Get-NetComputer -TrustedToAuth #Find computers with Constrined Delegation
Get-DomainGroup -AdminCount | Get-DomainGroupMember -Recurse | ?{$_.MemberName -like '*

# Logon and Sessions
<strong>
</strong>Get-NetLoggedon -ComputerName &#x3C;servername> #Get net logon users at the moment in a computer (need admins rights on target)
Get-NetSession -ComputerName &#x3C;servername> #Get active sessions on the host
Get-LoggedOnLocal -ComputerName &#x3C;servername> #Get locally logon users at the moment (need remote registry (default in server OS))
Get-LastLoggedon -ComputerName &#x3C;servername> #Get last user logged on (needs admin rigths in host)
Get-NetRDPSession -ComputerName &#x3C;servername> #List RDP sessions inside a host (needs admin rights in host)
</code></pre>



3. **Shared Files and Folders**

```powershell
Get-NetFileServer #Search file servers. Lot of users use to be logged in this kind of servers
Find-DomainShare -CheckShareAccess #Search readable shares
Find-InterestingDomainShareFile #Find interesting files, can use filters
```

4. **GPOs & OUs**

<pre class="language-powershell"><code class="lang-powershell"><strong>#GPO
</strong>Get-NetGPO #Get all policies with details
Get-NetGPO | select displayname #Get the names of the policies
Get-NetGPO -ComputerName &#x3C;servername> #Get the policy applied in a computer
gpresult /V #Get current policy

<strong># Enumerate permissions for GPOs where users with RIDs of > -1000 have some kind of modification/control rights
</strong>Get-DomainObjectAcl -LDAPFilter '(objectCategory=groupPolicyContainer)' | ? { ($_.SecurityIdentifier -match '^S-1-5-.*-[1-9]\d{3,}

<strong># ACL
</strong>Get-ObjectAcl -SamAccountName &#x3C;username> -ResolveGUIDs #Get ACLs of an object (permissions of other objects over the indicated one)
Get-PathAcl -Path "\\dc.mydomain.local\sysvol" #Get permissions of a file
Find-InterestingDomainAcl -ResolveGUIDs #Find intresting ACEs (Interesting permisions of "unexpected objects" (RID>1000 and modify permissions) over other objects
Find-InterestingDomainAcl -ResolveGUIDs | ?{$_.IdentityReference -match "RDPUsers"} #Check if any of the interesting permissions founds is realated to a username/group
Get-NetGroupMember -GroupName "Administrators" -Recurse | ?{$_.IsGroup -match "false"} | %{Get-ObjectACL -SamAccountName $_.MemberName -ResolveGUIDs} | select ObjectDN, IdentityReference, ActiveDirectoryRights #Get special rights over All administrators in domain
</code></pre>

5. **Domain Trust**

```
Get-NetDomainTrust #Get all domain trusts (parent, children and external)
Get-NetForestDomain | Get-NetDomainTrust #Enumerate all the trusts of all the domains found
Get-DomainTrustMapping #Enumerate also all the trusts
​Get-ForestGlobalCatalog #Get info of current forest (no external)
Get-ForestGlobalCatalog -Forest external.domain #Get info about the external forest (if possible)
Get-DomainTrust -SearchBase "GC://$($ENV:USERDNSDOMAIN)" 
​Get-NetForestTrust #Get forest trusts (it must be between 2 roots, trust between a child and a root is just an external trust)
​Get-DomainForeingUser #Get users with privileges in other domains inside the forest
Get-DomainForeignGroupMember #Get groups with privileges in other domains inside the forest

```

### Referances:

{% embed url="https://hackersinterview.com/oscp/oscp-cheatsheet-powerview-commands/" %}

{% embed url="https://github.com/swisskyrepo/PayloadsAllTheThings" %}

{% embed url="https://powersploit.readthedocs.io/en/latest/" %}
