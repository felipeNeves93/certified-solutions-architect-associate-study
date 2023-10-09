****
**Placement Groups**

* Sometimes you want control over the EC2 instance placement strategy
* The strategy can be defined using placement groups
* When you create a placement group, you specify one of the following strategies for the group:
    * **Cluster:** Clusters instances into a low latency group in a single AZ
    * **Spread:** Spreads instances across underlying hardware (max 7 instances per group per AZ) - Critical apllications
    * **Partition:** Spreads instances across many different partitions (which rely on different sets of racks) within an AZ. Scales to 100s of EC2 instances per group. (Hadoop, Cassandra, Kafka)
****

**Placement Groups: Cluster**

* **Pros:** Great Network (10 Gbps bandwidth between instances)
* **Cons:** If the rack fails, all instances fails at the same time
* **Use Case:** 
    * Big Data job that needs to complete fast
    * Application that need extremely low latency and high network throughput
****

**Placement Groups: Spread**

* **Pros:**
    * Can span across AZs
    * Reduced risk in simultaneous failure
    * EC2 instances are on different physical hardware
* **Cons:**
    * Limited to 7 instances per AZ per placement group
* **Use Case:**
    * Application that needs to maximize high avaliability
    * Critical applications where each instance must be isolated from failure from each other
****

**Placement Groups: Partition**

* Up to 7 partitions per AZ
* Can span across multiple AZs in the same region
* Up to 100s of EC2 instances
* The instances in a partition do not share racks with the instances in other partitions
* A partition failure can affect many EC2 but won't affect other partitions
* EC2 instances get access to the partition information as metadata
* **Use Cases:**
    * HDFS
    * Hbase
    * Cassandra
    * Kafka