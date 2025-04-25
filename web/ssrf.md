# SSRF

It is a type of attack that allows the attacker to cause the server-side application to make requests to unintended locations.

### Ways to attack SSRF:

1.  Cause the server to request content by providing its **loopback** address.

    **example :** http://localhost:8008/admin
2. Try to access other backend systems which are otherwise not accessible because of being present with a private **ip adress .**

### Bypassing Protection Mechanisms:

* **Use an alternative IP representation** of 127.0.0.1, such as 2130706433, 017700000001, or 127.1.
* Register your own domain name that resolves to 127.0.0.1. You can use spoofed.burpcollaborator.net for this purpose.
* Obfuscate blocked strings using URL encoding or case variation.
* Provide a URL that you control, which redirects to the target URL. Try using different redirect codes, as well as different protocols for the target URL. For example, switching from an http: to https: URL during the redirect has been shown to bypass some anti-SSRF filters.

#### 2. Whitelist-based input filters:

*

