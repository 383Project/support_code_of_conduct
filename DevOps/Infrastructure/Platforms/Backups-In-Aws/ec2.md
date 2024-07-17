# Back-ups in AWS
[Table of Contents](/readme.md)

## AWS Back-ups by service
[EC2](/DevOps/Infrastructure/backups-in-aws/ec2.md)
[RDS](/DevOps/Infrastructure/backups-in-aws/rds.md)
[S3](/DevOps/Infrastructure/backups-in-aws/s3.md)

## EC2 Back-ups

A back-up of an EC2 instance should be taken before any changes are made to the server OS or software packages or as part of scheduled maintenance as agreed with the client.

In AWS EC2 instances are backed-up using what Amazon calls, AMI's - Amazon Machine Image. This is a snapshot of an EC2 instance in it's current state and can be used to quickly and simply recreate that EC2 instance exactly as it is. We can also use these AMI's to recreate the EC2 instance on a larger server.

## Create an AMI

To create an AMI in AWS navigate to `EC2 > Instances`. Mark the check-box for the instance you wish to back-up, and under `Actions` select `image and templates > create image`.

Fill in the necessary details as follows;
`Image name` Should be something that relates to the reason for the backup if possible, and should always end with a timestamp as follows; `yyyymmdd_hhmm`. As an example a full image name might be `pre-node-intall-20230130_1355`.

`Image description - optional` Please enter the reason for the back up here.

Everything else should be left as default.

## Restore from AMI

Restore may be the wrong word, as we really create a new instance using our AMI. In AWS, navigate to `EC2 > Instances` and `Launch instances`. In another tab navigate to `EC2 > Instances` and click the `Instance ID` for your old server. We will use information in here to ensure that we set up the right Security Groups etc on the new server.

Enter a relevant name for the new server and then, under `Application and OS Images (Amazon Machine Image)` click on `My AMIs`. The drop-down menu will display all of the AMI's on the account. Find and select your required AMI.

`Instance type`: Select the right instance type to suit the requirements. This should match the previous server unless you are using the AMI for an upgrade. If in doubt, speak to DevOps.

`Key pair (login)` Select the key pair as used previously. Using a different key is likely to break deployements. The old key can be found by viewing the old instance (by clicking the `Instance ID` as mentioned earlier) and finding the `Key pair name` under `Details`.

![find previous key pair](/Assets/backups-in-aws/ec2/find-previous-key-pair.png)

`Network settings` Select all security groups as previously used. Again, the previous security groups can be found by viewing the old EC2 server. Security groups can be found under the `Security` tab. It's important to note both `Inbound rules` and `Outbound rules`.

![Security groups](/Assets/backups-in-aws/ec2/security-groups.png)

All other settings should be left as default. You can now `Launch instance`.