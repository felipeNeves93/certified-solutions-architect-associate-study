****
**RDS Overview**

* RDS stands for Relational Database Service
* It's a managed DB service for DB use SQL as query language
* It allows you to create databases in the cloud that are managed by AWS
    * Postgres
    * MySQL
    * MariaDB
    * Oracle
    * Microsoft SQL Server
    * Aurora (AWS Propietary)

**Advantages over using RDS versus deploying DB on EC2**

* RDS is a managed service
  * Automated provisioning
  * OS Patching
  * Continuous backups and restore to specific timestamp (Point In Time Restore)
  * Monitoring dashboards
  * Read replicas for improved read performance
  * Multi-AZ setup for DR (Disaster Recovery)
  * Maintance windows for upgrades
  * Scaling capability (Vertical/Horizontal)
  * Storage backed by EBS (gp2 or io1)
* You can't SSH into your instances
    
**Storage Auto Scaling**

* Helps you increase storage on your RDS DB instance dynamically
* When RDS detects you are running out of free database storage, it scales automatically
* Avoid manually scaling your database storage
* You have to set **Maximum Storage Treshold** (Maximum limit for DB storage)
* Automatically modify storage if:
  * Free storage is less than 10% of allocated storage
  * Low storage lasts at least 5 minutes
  * 6 hours passes since last modification  
* Useful for applications with **unpredictable workloads**
* Supports all RDS database engines (MariaDB, MySQL, PostgreSQL, SQL Server, Oracle)
****