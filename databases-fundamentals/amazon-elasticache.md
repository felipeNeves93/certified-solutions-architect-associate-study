****
**Amazon ElastiCache Overview**

* The same way RDS is to get managed Relational Databases
* ElastiCache is to get managed Redis or Memcached
* Caches are in-memory databases with really high performance, low latency
* Helps reduce load off of databases for read intensive workloads
* Helps make your application stateless
* AWS takes care of OS maintenance, patching, optimizations, setup, configuration, monitoring, failure recovery and backups
* **Using ElastiCache involves heavy application code changes**

**Solution Architecture**

* Applications queries ElastiCache, if not avaliable, get from RDS and store in ElastiCache
* Helps relieve load in RDS
* Cache must have an invalidation strategy to make sure only the most current data is used in there
* User logs into any of the application
* The application writes to the session data into ElastiCache
* The user hits another instance of the application
* The instance retrieves the data and the user is already logged in

**ElastiCache - Redis vs Memcached**

* **Redis:**
  * **Multi-AZ** with Auto-Failover
  * **Read Replicas** to scale reads and have **high avaliability**
  * Data Durability using AOF persistence
  * **Backup and restore features**
  * Supports Sets and Sorted Sets

* **Memcached**
  * Multi-node for partitioning of data (sharding)
  * **No high avaliability (replication)**
  * **Non Persistent**
  * **No Backup and Restore**
  * Multi-threaded architecture