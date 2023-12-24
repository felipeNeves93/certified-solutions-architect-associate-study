# Main Amazon S3 Concepts

### Security

* **User-Based**
  * **IAM Policies**: Which API calls should be allowed for specific user from IAM

* **Resource-Based**
  * **Bucket Policies**: Bucket wide rules from the S3 console - allows cross account
  * **Object Access Control List (ACL)**: Finer grain (can be disabled)
  * **Bucket Access Control List (ACL)**: less common (can be disabled)

* **Note:** An IAM principal can access an S3 object if:
  * The user IAM permissions ALLOW it OR the resource policy ALLOWS it
  * AND there is no explicit DENY

* **Encryption:** Encrypt objects in Amazon S3 using encryption keys 

### Bucket Policies

* JSON based policies
  * Resources: buckets and objects
  * Effect: Allow/Deny
  * Actions: Set of API or Allow or Deny
  * Principal: The account or user fo apply the policy to

* Use S3 bucket policy for:
  * Grant public access to the bucket
  * Force objects to be encrypted at upload
  * Grant access to another account (Cross Account)

* Bucket Setting for Block Public Access
  * These settings were created to prevent company data leaks

* Example of policy:
~~~
  {
    "Version": "2012-10-17",
    "Statement": [
        {
        "Effect": "Allow",
        "Principal": {
            "AuthenticatedUsers": ""
        },
        "Action": [
            "s3:GetObject",
            "s3:PutObject"
        ],
        "Resource": "arn:aws:s3:::your-bucket-name/*"
        }
  ]}
~~~

### Static Website Hosting

* S3 can host static websites and have them accessible on the Internet
* The website URL will be (depending on the region)
  * http://bucket-name.s3-website.aws.region.amazonaws.com
* If you get a **403 Forbidden** error, make sure the bucket policy allows public reads!

### Versioning 

* You can version your files in Amazon S3
* It is enabled at the **bucket level**
* Same key overwite will change the "version": 1,2,3
* It is best practice to version your buckets
  * Protect against unintended deletes (ability to restore a version)
  * Easy roll back to previous version
* Notes:
  * Any file that is not versioned prior to enabling versioning will have version "null"
  * suspending versioning does not delete the previous version

### Replication

* **Must enable versioning** in source and destination buckets
* **Cross Region replication (CRR)**
* **Same Region Replication (SRR)**
* Buckets can be in different AWS accounts
* Copying is Asyncrhonus
* Must give proper IAM permissions to S3
* Use Cases:
  * **CRR:** Compliance, lower latency access, replication across accounts
  * **SRR:** Log aggregation, live replication between production and test accounts
* After you enable Replication, only new objects are replicated
* Optionally, you can replicate existing objects using **S3 Batch Replication**
  * Replicates existing objects and objects that failed replication

* For DELETE operations
  * **Can replicate delete markers** from source to target (optional setting)
  * Deletions with a version ID are not replicated (to avoid malicious deletes)
* **There is no "chaining" of replication**
  * If bucket 1 has replication into bucket 2, which has replication into bucket 3
  * Then, objects created in buycket 1 are not replicated to bucket 3

### S3 Storage Classes

* Amazon S3 Standard - General Purpose
* Amazon S3 Standadrd-Infrequent Access (IA)
* Amazon S3 One Zoned-Infrequent Access
* Amazon S3 Glacier Instant Retrieval
* Amazon S3 Glacier Deep Archive
* Amazon S3 Intelligent Tiering

* Can move between classes manually or using S3 Lifecycle configurations

### Durability and Avaliability

* Durability:
  * High Durability (99,99999999999% 11 9's) of objects across multiple AZ
  * If you store 10,000,000 objects with Amazon S3, you can on average expect yo incur a loss of a single object once every 10,000 years
  * Same for all storage classes

* Avaliability:
  * Measures how readily avaliable a service is
  * Varies depending on storage class
  * Example: S3 standard has 99,99% avaliability: not avaliable 53 minutes a year

### S3 Infrequent Access

* For data that is less frequently accessed, but requires rapid access when needed
* Lower cost than S3 standard

* **Amazon S3 Standard-Infrquent Access (S3 Standard-IA)**
  * 99.9% Avaliability
  * Use Cases:
    * Disaster Recovery
    * Backups

* **Amazon S3 One Zone-Infrequent Access (S3 One Zone-IA)
  * High Durability (99.99999999999%) in a single AZ
  * Data Lost when AZ is destroyed
  * 99.5% Avaliability
  * Use Cases: Storing secondary backup copies of on-premise data, or data you can recreate

### S3 Glacier

* Low-cost object storage meant for archiving/backup
* Pricing: price for storage + object retrieval cost

* **Amazon S3 Glacier Instant Retrieval**
  * Milisecond retrieval, great for data accessed once a quarter
  * Minimun storage duration of 90 days
* **Amazon S3 Glacier Flexible Retrieval (Formerly Amazon S3 Glacier)**
  * Expedited (1 to 5 minutes), Standard (3 to 5 hours), Bulk (5 to 12 hours) - free
  * Minimun storage duration of 90 days
* **Amazon S3 Glacier Deep Archive - for long term storage
  * Standard (12 Hours), Bulk (48 hours)
  * Minimun storage duration of 180 days

### S3 Inteligent-Tiering

* Small monthly monitoring and auto-tiering fee
* Moves objects automatically between Access Tiers based on usage
* There are no retrieval charges in S3 Inteligent-Tiering

* Frequent Access tier (automatic): default tier
* Infrequent Access Tier (automatic): Objects not accessed for 30 days
* Archive instant Access Tier (automatic): objects not accessed for 90 days
* Archive Access Tier (Optional): Configurable from 90 days to 700+ days
* Deep Archive Access Tier (Optional) Config from 180 days to 700+ days