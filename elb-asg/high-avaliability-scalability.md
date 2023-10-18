****
**Scalability and High Avaliability**

* Scalability means that an application / system can handle greater loads by adapting
* There are two kinds of scalability:
    * Vertical Scalability 
    * Horizontal Scalability (Elasticity)
* **Scalability is linked but different to High Avaliability**
****

**Vertical Scalability**

* Vertical scalability means increasing the size of the instance
* For example, your application runs on a t2.micro
* Scaling the application vertically means running it on a t2.large
* Vertical Scalability is very common for non distributed systems such as a database
* RDS, ElastiCache are services that can scale vertically
* There's usually a limit to how much you can vertically scale (Hardware Limit)
****

**Horizontal Scalability**

* Horizontal Scalability means increasing the number of instances / systems for your application
* Horizontal scaling implies distributed systems
* This is very common for modern applications / web applications
* Its easy to horizontal scale thanks to cloud providers like Amazon EC2
****

**High Avaliability**

* High Avaliability usually goes hand in hand with horizontal scalling
* High Avaliability means running your application / system in at least 2 data centers (AZs)
* The goal of High Avaliability is to survive a data center loss
* The high avaliability can be passive (For RDS Multi AZ for example)
* The High avaliability can be active (For horizontal scaling)
****

**High Avaliability and Scalability for EC2**

* Vertical Scaling: Increase instance size (scale up/down)
    * From: t2.nano - 0.5G of RAM, 1 vCPU
    * To: u-12tb1.metal - 12.3TB of RAM, 448 vCPUs

* Horizontal Scaling: Increase number of instances (Scale out/in)
    * Auto Scaling Group
    * Load Balancer

* High Avaliability: Run instances for the same application across multiple AZ
    * Auto Scaling Group multi AZ
    * Load Balancer multi AZ

