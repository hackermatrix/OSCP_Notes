# 500 - IKE/IPsec

#### 1. IKE Scan:

**IKE(Internet Key Exchange)** Scan is used to discover IKE hosts and also fingerprints them using the re-transmission backoff pattern. IKE Scan discovers the hosts running by IKE. IKE scan sends requests to the IKE and shows the hosts who responded to the request from IKE.

* IKE has two phases, _**phase 1**_ is responsible for setting up and establishing secure authenticated communication channel, and _**phase 2**_ encrypts and transports data.

Our focus of interest here would be _phase 1_; it uses two methods of exchanging keys:

* Main mode
* Aggressive mode

To scan a host for an aggressive mode handshake, use the following commands:

<pre class="language-markup"><code class="lang-markup"><strong>ike-scan x.x.x.x -M -A
</strong></code></pre>

Sometimes we will see the response after providing a valid group name like (vpn):

<pre class="language-markup"><code class="lang-markup"><strong> ike-scan x.x.x.x -M -A id=vpn
</strong></code></pre>

> We can even brute force the group names using the following&#x20;
>
> script: [https://github.com/SpiderLabs/groupenum](https://github.com/SpiderLabs/groupenum).[https://github.com/SpiderLabs/groupenum](https://github.com/SpiderLabs/groupenum)&#x20;
>
> The command:`./dt_group_enum.sh x.x.x.x groupnames.dic`

2. **Cracking the PSK**

To learn how to crack the PSK follow the given steps:

1. Adding a `-P` flag in the `ike-scan` command it will show a response with the captured hash.
2. To save the hash we provide a filename along with the `-P` flag.
3. Next we can use the `psk-crack` with the following command:

<pre class="language-markup"><code class="lang-markup"><strong>psk-crack -b 5 /path/to/pskkey
</strong></code></pre>

4. Where `-b` is brute force mode and length is `5`.
5. To use a dictionary based attack we use the following command:

<pre class="language-markup"><code class="lang-markup"><strong>psk-crack -d /path/to/dictionary /path/to/pskkey
</strong></code></pre>

The following screenshot shows the output for the preceding command:

![](https://i0.wp.com/hackonology.com/wp-content/uploads/2020/11/ike-bruteforce.png?resize=624%2C68\&ssl=1)

#### How it works…

In aggressive mode the authentication hash is transmitted as a response to the packet of the VPN client that tries to establish a connection Tunnel (IPSEC). This hash is not encrypted and hence it allows us to capture the hash and perform a brute force attack against it to recover our PSK.

This is not possible in main mode as it uses an encrypted hash along with a six way handshake, whereas aggressive mode uses only three way.

#### References (In Sequence):

{% embed url="https://aws.amazon.com/what-is/ipsec/" %}

{% embed url="https://www.techtarget.com/searchsecurity/definition/Internet-Key-Exchange" %}

{% embed url="https://book.hacktricks.xyz/network-services-pentesting/ipsec-ike-vpn-pentesting" %}
