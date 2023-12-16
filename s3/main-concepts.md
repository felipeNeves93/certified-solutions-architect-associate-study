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

