****
**What is an Auto Scaling Group?**

* In real life, the load on your websites and applications can change
* In the cloud, you can create amd get rid of servers very quickly
* The goal of an Auto Scaling Group (ASG) is to:
  * Scale out (add EC2 instances) to match an increased load
  * Scale in (remove EC2 instances) to match a decreased load
  * Ensure we have a minimum and maximum number of EC2 instances running
  * Automatically register new instances to a load balancer
  * Re-create an EC2 instance in case a previous one is terminated (ex: if unhealthy)
* **ASG are free (you only pay for the underlying EC2 instances)**

**Auto Scaling Group Attributes**

* A **Launch Template** (older "Launch Configurations" are deprecated)
  * AMI + Instance Type
  * EC2 User Data
  * EBS Volumes
  * Security Groups
  * SSH Key Par
  * IAM Roles for your EC2 Instances
  * Networks + Subnets information
  * Load Balancer Informations
* Min Size/Max Size/Initial Capacity
* Scaling Policies

**Auto Scaling - CloudWatch Alarms & Scaling**

* It is possible to scale an ASG based on CloudWatch alarms
* An alarm monitors a metric (such as **Average CPU**, or a **custom metric**)
* **Metrics such as Average CPU are computed for the overall ASG instances**
* Based on the alarm:
  * We can create scale-out policies (increase the number of instances)
  * We can create scale-in policies (decrease the number of instances)