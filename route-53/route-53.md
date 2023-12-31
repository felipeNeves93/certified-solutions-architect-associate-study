****
### What is Amazon Route 53?

* A highly avaliable , scalable, fully managed and Authoritative DNS
  * Authoritative = the costumer (you) can update the DNS records
* Route 53 is also a Domain Registrar
* Ability to check the health of your resources
* The only AWS service that offers 100% avaliability SLA
* Why Route 53? 53 is a reference to the traditional DNS Port

### Route 53 records

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

### Record Types

* **A:** Maps a hostname to IPv4
* **AAAA:** Maps a hostname to IPv6
* **CNAME:** Maps a hostname to another hostname
  * The target is a domain name which must have an A or AAAA record
  * Can't create a CNAME record for the top node of a DNS namespace (Zone Apex)
  * Example: You can't create for example.com but you can create to www.example.com
* **NS: Name Servers for the Hosted Zone**
  * Controls how traffic is routed for a domain

### Hosted Zones

* A container for records that define how to route traffic to a domain and its subdomains
* **Public Hosted Zones:**
  * Contains records that specify how to route traffic on the internet(public domain names)
  * *application1.mypublicdomain.com*
* **Private Hosted Zones:**
  * Contains records that specify how you route traffic within one or more VPCS (private domain names)
  * *application1.company.internal

### Records TTL (Time to Live)

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

###CNAME vs ALIAS

* AWS resources (Load Balancer, Cloudfront, etc) expose an AWS Hostname
  * *lb1-1234.us.east-2.elb.amazonaws.com* and you want *myapp.mydomain.com*
* CNAME
  * Points a hostname to any other hostname. (app.mydomain.com -> blablabla.anything.com)
  * **Only for ROOT DOMAIN and NON ROOT DOMAIN  (aka mydomain.com)
  * Free of charge
  * Native health check

### Alias Records

* Maps a hostname to an AWS resource
* An extension to DNS functionality
* Automatically recognizes changes in the resource's IP addresses
* Unlike CNAME, it can be used for the top node of a DNS namespace (Zone Apex) e.g: example.comn
* Alias Record is always of the type A/AAAA for AWS resources (IPv4, IPv6)

### Alias Records Targets

* Elastic Load Balancers
* CloudFront distributions
* API Gateway
* Elastic Beanstalk environments
* S3 Websites
* VPC interface endpoints
* Global Accelerator accelerator
* Route 53 record in the same hosted zone
* **You cannot set an ALIAS record for an EC2 dns Name

### Routing Policies

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

### Routing Policies - Simple

  * Typically route traffic to a single resource
  * Can specify multiple values in the same record
  * **If multiple values are returned, a random one is chosen by the client**
  * When Alias enabled, specify only one AWS resource
  * Can't be associated with Health Checks

### Routing Policies - Weighted

  * Control the % of the requests that go to each specific resource
  * Assign each record a relative weight
    * **Traffic (%) = wheight for a specific record/Sum of all the weights for all the records**
    * Weights don't need to sum up to 100
  * DNS Records must have the same name and type
  * Can be associated with Health Checks
  * Use cases: 
    * Load balancing between regions
    * testing new application versions
  * **Assign a weight of 0 to a record to stop reading traffic to a resource**
  * **If all records have weight of 0, then all records will be returned equally**

### Routing Policies - Latency based

  * Redirect to the resource that has the least latency close to us
  * Super helpful when latency to users is a priority
  * **Latency is based on traffic between users and AWS regions** 
  * Germany users may be directed to the US (if that's the lowest latency)
  * Can be associated with health checks (has a failover capability)

### Health Checks

  * HTTP Health Checks are only for **public resources**
  * Health Check - Automated DNS failover
    * Health checks that monitor an endpoint (Application, servers, other AWS resources)
    * Health Checks that monitor other health checks (Calculated Health Checks)
    * Health checks that monitor CloudWatch Alarms (full control) e.g. throttles of DynamoDB,
    alarms on RDS, custom metrics... helpfull for private resources
  * Health Checks are integrated with CW metrics
   
### Health Checks - Monitor an endpoint

* **About 15 Global Health Checkers will check the endpoint health**
  * Healthy/Unhealthy Threshold - 3 (default)
  * Interval - 30 sec (Can set to 10 sec - higher cost)
  * Supported protocol: HTTP, HTTPS and TCP
  * IF > 18% of health checkers report the endpoint is healthy, Route 53 considers **Healthy**
  * Otherwise is considered **Unhealthy**
  * Ability to choose which location you want Route53 to use
* Health Checks pass only when the endpoint responds with the 2xx and 3xx status codes
* Health Checks can be setup to fail/pass based on the text in the first **5120 bytes** of the response
* Configure your router/firewall to allow incoming requests from Route53 Health Checkers

### Calculated Health Checks

* Combine the results of multiple Health Checks into a single Health Check
* You can use **OR, END,** or **NOT**
* Can monitor up to 256 child health checks
* Specify how many health checks need to pass to make the parent pass
* Usage: Perform maintenance to your website without causing all health checks to fail

### Health Checks - Private Hosted Zones

* Route53 Health Checkers are outside the VPC
* They can't access **private** endpoints (private VPC or on-permisse resources)
* You can create a **CloudWatch metric** and associate a **CloudWatch Alarm**, then create a health check that checks the alarm itself 

### Domain Registar vs DNS Service

* You buy or register your domain name with a Domain Registar typically by paying annual charges (GoDaddy, Amazon Registar Inc, etc...)
* The Domain Registar usually provides you with DNS service to manage your DNS records
* But you can use another DNS service to manage your DNS records
* Example: Purchase the domain from GoDaddy and use Route 53 to manage your DNS records

### 3rd Party Registar with Amazon Route 53

* **If you buy your domain on a 3rd party registrar, you can still use Route 53 as the DNS Service Provider**
    * Create a Hosted Zone in Route 53
    * Update NS Records on 3rd Party website to use Route 53 **Name Servers**
  * **Domain Registrar != DNS Service**
  * But every Domain Registrar usually comes with some DNS features