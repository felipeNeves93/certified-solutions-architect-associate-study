****
**What is Amazon Route 53?**

* A highly avaliable , scalable, fully managed and Authoritative DNS
  * Authoritative = the costumer (you) can update the DNS records
* Route 53 is also a Domain Registrar
* Ability to check the health of your resources
* The only AWS service that offers 100% avaliability SLA
* Why Route 53? 53 is a reference to the traditional DNS Port

**Route 53 records**

* How you want to route traffic for a domain
* Each record contains:
  * **Domain/subdomain Name:** e.g. example.com
  * **Record Type:** e.g. A or AAA
  * **Value:** e.g. 12.34.56.78
  * **Routing Policy:** How Route 53 respond to queries 
  * **TTL:** Amount of time the record cached at DNS Resolvers
* Route 53 supports the following DNS record types:
  * (Must Know) **A / AAAA / CNAME / NS**
  * (Advanced) **CAA / DS / MX / NAPTR / PTR / SOA / TXT / SPF / SRV** 

**Record Types**

* **A:** Maps a hostname to IPv4
* **AAAA:** Maps a hostname to IPv6
* **CNAME:** Maps a hostname to another hostname
  * The target is a domain name which must have an A or AAAA record
  * Can't create a CNAME record for the top node of a DNS namespace (Zone Apex)
  * Example: You can't create for example.com but you can create to www.example.com
* **NS: Name Servers for the Hosted Zone**
  * Controls how traffic is routed for a domain

**Hosted Zones**

* A container for records that define how to route traffic to a domain and its subdomains
* **Public Hosted Zones:**
  * Contains records that specify how to route traffic on the internet(public domain names)
  * *application1.mypublicdomain.com*
* **Private Hosted Zones:**
  * Contains records that specify how you route traffic within one or more VPCS (private domain names)
  * *application1.company.internal