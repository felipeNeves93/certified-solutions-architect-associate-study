****
**What is an EBS Volume?**

* An **EBS (Elastic Block Store) Volume** is a **Network Drive** you can attach to your instances while they run
* It allows your instances to persist data, even after their termination
* **They can only be mounted to one instance at a time** (at the CCP level)
* They are bound to a **specific AZ**
* Analogy: Think of them as  a "network USB stick"
* Free tier: 30 GB of free EBS Storage of type General Purpose (SSD) or Magnetic per month
****

**EBS Volume**

* **It's a Network drive (i.e not a physical drive)**
    * It uses the network to communicate the instance, which means there might be a bit of latency
    * It can be detached from one EC2 instance to another quickly
* **It's locked to an AZ**
    * An EBS volume in us-east-1a cannot be attached to us-east-1b 
    * To move a volume accross first you need to snapshot it
* **Have a provisioned capacity (size in GBs and IOPS)**
    * You get billed for all the provisioned capacity
****

**EBS Delete on Termination attribute**

* Controls the EBS behavior when an EC2 instance is terminated
    * By default, the root EBS volume is deleted (attribute enabled)
    * By default, any other attached EBS Volume is not deleted (attribute disabled)
* This can be controlled by the AWS Console / AWS CLI
* **Use case: Preserve root volume when instance is terminated**