# Architecture Discussion: Whats The Time

* It allows people to know what time it is
* A database isn't needed
* Will start small and can accept downtime
* Will be fully scaled horizontally and vertically, no downtime
* Will contain the view of a Solutions Architect fitting the components together.

## Types of Solutions

#### Vertical Scaling With Elastic Ip attached to it?

* Not good solution, will have downtime when scales vertically
* Not cost friendly

#### Horizontal Scaling with Elastic Ips Single AZ

* The scaling is correct
* User would have to know all the new ips when scaling

#### Using Route 53 Single AZ

* The elastic ip problem is solved, no more elastic ip
* A Dns query would be send for api.whatisthetime.com
* It would be an A record
* Time To Live (TTL) of 1 hour
* The problem is when an instance dies, because the TTL is of 1 hour, the query would be sent to an non-existant instance

#### Private EC2 instances with ELB + Route 53 Single AZ

* An alias record would be utilized by Route 53 queries
* The users would be redirected to the Load Balancer
* Load balancer would distribute the traffic
* No downtime
* The problem is manually adding and removin instances is cumbersome

#### Private EC2 instances With ELB + Route 53 + Auto Scalling Group Single AZ

* Has the same benefits of the previous topic
* Has no problem with manually adding/removing instances
* Needs to be splitted across multi-Azs

#### Private EC2 instances With ELB + Route 53 + Auto Scalling Group Multi-AZ

* Minimum 2 AZs
* Think about cost savings, use reserved instances 

## Topics Discussed in this architecture

* Public vs Private IP and EC2 Instances
* Elasitc IP vs Route 53 vs Load Balancers
* Route 53 TTL, A records and Alias Records
* Maintaining EC2 instances manually vs Auto Scaling Groups
* Multi-AZ to survive disasters
* ELB Health Checks
* Security Group Rules
* Reservation of capacity for costing saving whenever possible
* We considered 5 pillars for a well architected application:
  * Cost
  * Performance
  * Reliability
  * Security
  * Operational Excelence