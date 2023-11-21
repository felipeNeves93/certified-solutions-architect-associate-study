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

**Records TTL (Time to Live)**

* **High TTL:**
  * 24 hr
  * Less traffic on Route 53
  * Possibly outdated records
* **Low TTL:**
  * 60 Sec
  * More traffic on Route 53 ($$)
  * Records are outdated for less time
  * Easy to change records
* **Except for Alias records, TTL is mandatory for each DNS record**

**CNAME vs ALIAS**

* AWS resources (Load Balancer, Cloudfront, etc) expose an AWS Hostname
  * *lb1-1234.us.east-2.elb.amazonaws.com* and you want *myapp.mydomain.com*
* CNAME
  * Points a hostname to any other hostname. (app.mydomain.com -> blablabla.anything.com)
  * **Only for ROOT DOMAIN and NON ROOT DOMAIN  (aka mydomain.com)
  * Free of charge
  * Native health check

**Alias Records**

* Maps a hostname to an AWS resource
* An extension to DNS functionality
* Automatically recognizes changes in the resource's IP addresses
* Unlike CNAME, it can be used for the top node of a DNS namespace (Zone Apex) e.g: example.comn
* Alias Record is always of the type A/AAAA for AWS resources (IPv4, IPv6)

**Alias Records Targets**

* Elastic Load Balancers
* CloudFront distributions
* API Gateway
* Elastic Beanstalk environments
* S3 Websites
* VPC interface endpoints
* Global Accelerator accelerator
* Route 53 record in the same hosted zone
* **You cannot set an ALIAS record for an EC2 dns Name

**Routing Policies**

* Define how Route 53 responds to DNS queries
* Don't get confused by the word Routing
  * It's not the same as Load Balancer routing which routes the traffic
  * DNS does not route any traffic, it only responds to the DNS queries
* Route 53 Supports the following Routing Policies
  * Simple
  * Weighet
  * Failover
  * Latency Based
  * Geolocation
  * Multi-Value Answer
  * Geoproximity (Using Route 53 Traffic Flow Feature)

**Routing Policies - Simple**

* Typically route traffic to a single resource
* Can specify multiple values in the same record
* **If multiple values are returned, a random one is chosen by the client**
* When Alias enabled, specify only one AWS resource
* Can't be associated with Health Checks