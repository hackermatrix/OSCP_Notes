# Certificate Transparency

> Certificate Transparency(CT) is a project under which a Certificate Authority(CA) has to publish every SSL/TLS certificate they issue to a public log. An SSL/TLS certificate usually contains domain names, sub-domain names and email addresses.
>
> ([blog.appsecco.com](https://blog.appsecco.com/))

The following websites allow to search through their CT logs: [crt.sh](https://crt.sh/), [censys.io](https://censys.io/), [Facebook's CT monitor](https://developers.facebook.com/tools/ct/), [Google's CT monitor](https://transparencyreport.google.com/https/certificates).

[Findomain](https://github.com/Findomain/Findomain) (Rust), [Subfinder](https://github.com/projectdiscovery/subfinder) (Go) and [Assetfinder](https://github.com/tomnomnom/assetfinder) (Go) mainly rely on Certificate Transparency logs enumeration.

```bash
# Standard enumeration with findomain
findomain -t "target.domain" -a

# Standard enumeration with subfinder
subfinder -d "target.domain"

# Pipe subfinder with httpx to find HTTP services
echo "target.domain" | subfinder -silent | httpx -silent

# Standard enumeration with assetfinder
assetfinder "target.domain"
```
