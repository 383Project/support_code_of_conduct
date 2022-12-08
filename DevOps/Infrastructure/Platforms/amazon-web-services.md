# Platforms
[Table of Contents](/readme.md)
- [Amazon Web Services](./amazon-web-services.md)
- [Rackspace](./rackspace.md)

## Amazon Web Services

### What is AWS?
AWS is a hosting solution where Amazon manages and administrates a magantude of different services ranging from typical blade style servers to Content Delivery Networks, massive storage solutions and serverless technologies. This suite of technologies is commonly referred to as "The Cloud".

### Why we use AWS
AWS provides a large range of technical solutions and it's suite is ever increasing in scope and scale, however AWS' biggest strength in it's ability to be plugged into other technical solutions via it's API.

Utilising AWS' API we've been able to create the [AWS Server Tracker](https://docs.google.com/spreadsheets/d/1MM4LabigHVVRLJmt-97n4RoL7gYdkUGy3dFZiN1iIM8/edit#gid=0) which using Google's Sheets and Scripts allows us to check on the status of servers in real time, and monitor the costs incurred on the various accounts we manage.

### Elastic Cloud Compute (EC2)
This service is the typical server blade setup. EC2 servers, or instances using AWS' terminology, are typically configured using their own Amazon Linux 2 distribution, or the latest supported version of Ubuntu. This is determined by the needed services of Engineering.

If Engineering requires PHP 8.0 or above then Ubuntu is the go to Linux distribution as Amazon's package managers do not support any version of PHP above 7.4 as of the 30th of November 2022.

Instance size for the EC2 should be dictated by the [hosting estimate](./hosting-estimates.md) of the work to be done.

### Relational Database Service (RDS)
This service is our go to for a database solution. RDS effectively runs a separate server explicitly to host a database. Typically we run MySQL 5.7 or 8.0 depending on the needs of Engineering. Backups are configured to run daily and held for the maximum value of 35 days. Instance sizes are set to t2.micro or t3.micro as the volume of traffic is low enough to not warrent anything larger.