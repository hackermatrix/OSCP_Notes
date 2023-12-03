# Recon

1. IP space discovery (ASN):
2. Subdomain Enumeration:
   1. **Passive techniques:**
      1. [certificate-transparency.md](certificate-transparency.md "mention")
      2. ASN Discovery
      3. Search engines (Google & Bing Dorking)
      4. DNS aggregators/datasets (Github, Virustotal, DNSdumpster etc)
      5. Subject alternate name (SAN)
      6. Using public datasets
      7. DNS enum using Cloudflare
   2.  **Active techniques:**

       * HTTP virtual host fuzzing
       * HTTP headers
       * DNS zone transfers
       * DNS bruteforcing
       * DNS zone walking
       * DNS cache snooping
       * DNS records (CNAME, SPF)
       * Reverse DNS sweeping


3. Dorking:
   1. [github-recon.md](github-recon.md "mention")
   2. [google-dorks.md](google-dorks.md "mention")
4. Content Discovery
5. Parameter Discovery