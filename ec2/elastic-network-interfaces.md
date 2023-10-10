**Elastic Network Interfaces (ENI)**

* Logical component in a VPC that represents a **Virtual Network Card** 
* The ENI can have the following attributes:
    * Primary Private IP (IPV4), one or more secundary IPV4
    * One Elastic IP(IPV4) per private IPV4
    * One public IPV4
    * One or more security groups
    * A MAC address
* You can create ENI independently and attach then on the fly (move then) on EC2 instances 
for failover
* Bound to specific AZ