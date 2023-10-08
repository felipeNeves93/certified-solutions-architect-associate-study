****
**AWS Regions**

* AWS has **Regions** all around the world
* Names can be us-east-1, eu-west-3...
* A region is a **cluster of data centers**
* **Most AWS Services are region scoped**
****

**How to choose an AWS Region?**

* **Compliance with data governance and legal requirements:** Data never leaves a region without your explicit permission
* **Proximity to customers:** Reduced latency
* **Avaliable services within a Region:** New services and new features aren't avaliable in every Region
* **Pricing:** Pricing varies region to region and is transparent in the service pricing page
****

**AWS Avaliability Zones**

* Each region has many avaliability zones (usually 3, min is 3, max is 6) Example:
    * ap-southeast-2a
    * ap-southeast-2b
    * ap-southeast-2c
* Each avaliability zone (AZ) is one or more discrete data centers with redundant power, networking and connectivity
* They are separate from each other, so that they are isolated from disasters
* They are connected with high bandwidth, ultra-low latency networking
****

**AWS Points of presence(Edge Locations)**

* Amazon has 400+ Points of Presence (400* Edge Locations & 10+ Regional Caches) in 90+ cities across 40+ countries
* Content is delivered to end users with lower latency 
****

**AWS Scope of Services**

* **AWS has Global Services**
    * Identity and Access Management (IAM)
    * Route 53 (DNS Service)
    * CloudFront (Content Delivery Network)
    * WAF (Web Application Firewall)
* **Most AWS services are Region-scoped**
    * Amazon EC2 (Infrastructure as a Service)
    * Elastic Beanstalk (Platform as a Service)
    * Lambda (Function as a Service)
    * Rekognition (Software as a Service)
* **Region Table:** https://aws.amazon.com/abou-aws/global-infrastructure/regional-product-services