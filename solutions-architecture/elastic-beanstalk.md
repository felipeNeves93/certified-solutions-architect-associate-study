# Elastic Beanstalk

### Developers problems on AWS

* Managing infrastructure
* Deploying Code
* Configuring all the databases, load balacers, etc
* Scaling concerns
* Most web apps have the same architecture (ELB + ASG)
* All the developers want is for their code to run!
* Possibly, consistently across different applications and environments

### Elastic Beanstalk Overview

* Elastic Beanstalk is a developer centric view of deploying applications on AWS
* It uses all the components that we saw before
* Managed Service:
  * Automatically handles capacity provisioning, Load Balancing, Scaling, Application health monitoring, Instance Configuration.
  * Just the application code is responsability of the developer
* We still have full control over the configuration
* Beanstalk is free, but you pay for the underlying resources created

### Components

* **Application:** Collection of Elastic Beanstalk components: (Environments, versions, configurations)
* **Application Version:** An interation of your application code
* **Environment:** 
  * Collection of applications resources running an application version (Only one application version at a time)
  * **Tiers:** Web Server environment Tier and Work Environment Tier
  * You can create multiple environments: Dev, Test, Staging    
* Cycle: Create Application -> Upload Version -> Launch Environment -> Manage Environment

### Supported Platforms:

  * Go
  * Java SE
  * Java With Tomcat
  * .Net core on Linux
  * .Net on Windows Server
  * NodeJS
  * PHP 
  * Python
  * Ruby
  * Packer Builder
  * Single Container Docker
  * Multi Container Docker
  * Preconfigured Docker
  * If not supported, you can write your custom platform