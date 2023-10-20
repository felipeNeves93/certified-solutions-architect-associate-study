****
**Network Load Balancer (v2)**

* Network Load Balancers (Layer 4) allow to:
    * **Forward TCP and UDP traffic to your instances**
    * Handle millions of request per seconds
    * Letss latency ~100 ms vs 400 ms for ALB
* **NLB has one static IP per AZ, and supports assigning Elastic IP** (helpful for whitelisting specific IP)
* NLB are used for exteme performance, TCP or UDP traffic
* Not included in the AWS free tier


**Target Groups**

* EC2 instances
* IP Addresses - Must be private IPs
* Application Load Balancer
* Health Checks support the **TCP, HTTP and HTTPS Protocols**
****