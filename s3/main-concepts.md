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