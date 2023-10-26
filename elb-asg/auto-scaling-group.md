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
****
**Dynamic Scaling Policies**

* **Target Tracking Scaling**
  * Most simple and easy to set-up
  * Example: I want the ASG CPU to stay at around 40%
* **Simple / Step Scaling**
  * When a CloudWatch alarm is triggered (example CPU > 70%), then add 2 units
  * When a CloudWatch alarm is triggered (example CPU < 30%), ten remove 1
* **Schedule Actions**
  * Anticipate a scaling based on known usage patterns
  * Example: Increase the min capacity to 10 at 2 pm on Fridays
* **Predictive Scaling**
  * Continuosly forecast load and shcedule scaling ahead

**Good metrics to scale on**

  * **CPUUtilization:** Average CPU utilization across your instances
  * **RequestCountPerTarget:** To make sure the number of requests per EC2 instances is stable
  * **Average Network In / Out:** If your application is network bound
  * **Any custom metric:** That are pushed using CloudWatch

**Scaling Cooldowns**

* After a scaling activity happens, you are in the **cooldown period (default is 300 seconds)**
* During the cooldown period, the ASG will not launch or terminate additional instances (to allow for metrics to stabilize)
* Advice: Use a ready-to-use AMI to reduce configuration time in order to be serving request fasters and reduce the cooldown period