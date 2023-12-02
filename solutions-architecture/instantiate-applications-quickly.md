# How to Instantiate Applications Quickly

* EC2 Instances:
  * **Using Golden AMI:** Install your applications, OS dependencies, etc.. beforehand and launch your EC2 instance from the Golden AMI
  * **Bootstrap using User Data:** For dynamic configuration, use User Data Scripts
  * **Hybrid:** Mix Golden AMI and User Data (Elastic Beanstalk)

* RDS Databases:
  * Restore from a Snapshot: The database will have schemas an data ready

* EBS Volumes: 
  * Restore from a Snapshot: The disk will already be formatted and have data