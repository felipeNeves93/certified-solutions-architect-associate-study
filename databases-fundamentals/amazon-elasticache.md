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

**Cache Security**

* ElastiCache supports **IAM Authentication for Redis**
* IAM policies on ElastiCache are only used for AWS API-level security
* **Redis AUTH**
  * You can set a password/token when you create a Redis cluster
  * This is an extra level of security for your cache (on top of security groups)
  * Supports SSL in flight encryption
* Memcached
  * Supports SASL-based authentication (advanced) 

**Patterns for ElastiCache**

* **Lazy Loading:** All the read data is cached, data can become stale in cache
* **Write Through:** Adds or update data in the cache when written to a DB (no stale data)
* **Session Store:** store temporary session data in cache (using TTL features)

**Redis Use Case**

* Gaming Leaderborads are computationally complex
* **Redis Sorted Sets** guarantee both uniqueness and element ordering
* Each time a new element added, it's ranked in real time, then added in correct order
* ****