# Amazon S3 Overview

### Introduction

* Is one of the main building blocks of AWS
* Advertised as "infinitely scaling" storage
* Many websites use Amazon S3 as backbone
* Many AWS services use Amazon S3 as an integration as well

### Use Cases

* Backup and storage
* Disaster Recovery
* Archive
* Hybrid Cloud storage
* Application hosting
* Media Hosting
* Data Lakes and big data analytics
* Software Delivery
* Static Website

## Buckets

* Amazon S3 allows people to store objects (files) in "buckets" (directories)
* Buckets must have a **globally unique name (across all regions and all acounts)**
* Buckets are defined at the region level
* S3 looks like a global service, but buckets are created in a region
* Naming convention
  * No uppercase, No underscore
  * 3-63 characters long
  * Not an IP
  * Must start with lowercase letter or number
  * Must NOT start with prefix **xn-**
  * Must NOT end with the suffix **-s3alias**

### Objects

* Objects (files) have a key
* The key is the **FULL** path
  * s3://my-bucket/myf_file.txt
  * s3://my-bucket/my_folder1/another_folder/my_file.txt
* There's no concept of "directories" within buckets (Although the UI will trick you to think otherwise)
* Just keys with very long names that contain slashes("/")

### Objects (cont.)

* Object values are the content of the body:
  * Max Object Size is 5TB
  * If uploading more than 5GB, mus use "multi-part-upload"
* Metadata (list of text key / valuye par - up to 10) useful for security / lifecycle
* Version ID (if versioning is enabled)