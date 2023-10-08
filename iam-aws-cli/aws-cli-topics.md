****
**How can users access AWS?**

* To access AWS, you have three options:
    * AWS Management Console (Protected by password + MFA)
    * AWS Command Line Interface (CLI): Protected by access keys.
    * AWS SDK - For code: protected by access keys
* Access keys are generated through the AWS Console
* Users manage their own access Keys
* Access keys are secrets, just like passwords, don't share them
* Access Key ID ~= username
* Secret Access Key ~= password
****

**What is AWS CLI?**

* A tool that enables you to interact with AWS services using commands in your command-line shell
* Direct access to the public APIs of AWS services
* You can develop scripts to manage your resources
* It's open-source https://github.com/aws/aws-cli
* Alternative to using AWS Management Console
****

**What is AWS SDK?**

* AWS Software Development KIT (AWS SDK)
* Language-Specific API'S (set of libraries)
* Enables you to access and manage AWS services programmatically
* Embedded within your applications
* Supports:
    * SDSs(JavaScript, Python, PHP, .NET, Ruby, Java, Go, Node.js, C++)
    * Mobile SDKs (Android, iOS...)
    * IoT Device SKDs (Embedded C, Arduino...)
* Example: AWS CLI is built on AWS SDK for Python
****