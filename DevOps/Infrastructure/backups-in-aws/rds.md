# Backups in AWS
[Table of Contents](/readme.md)

## AWS Backups by service
[EC2](/DevOps/Infrastructure/backups-in-aws/ec2.md)
[RDS](/DevOps/Infrastructure/backups-in-aws/rds.md)
[S3](/DevOps/Infrastructure/backups-in-aws/s3.md)

## RDS Backups

There are two ways in which we take backups of databases. The first is through automated backups in AWS, while the other is a manual backup taken in TablePlus.

## Automated Backups - AWS

Turned on by default, the automated backup feature of Amazon RDS will backup your databases and transaction logs. Amazon RDS automatically creates a storage volume snapshot of your DB instance, backing up the entire DB instance and not just individual databases. This backup occurs during a daily user-configurable 30 minute period known as the backup window. Automated backups are kept for a configurable number of days (called the backup retention period). Your automatic backup retention period can be configured to up to thirty-five days.

In most cases we will utilise the maximum 35 day retention period. The 30 minute backup window is also configurable, however we usually leave this at default. [This window is selected at random from an 8-hour block of time for each AWS Region.](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_WorkingWithAutomatedBackups.html)

We can verify the retention period and access our backups by navigating to `RDS > Databases`, selecting the relevant database, and clicking the `Maintenance & backups` tab.

![rds automated backups](/Assets/backups-in-aws/rds/rds-auto-backups.png)

We can also modify the retention period and more from here by clicking the `Modify` button in the top right corner. At the bottom of the following page are the `Backup` and `Maintenance` settings.

![modify-backups](/Assets/backups-in-aws/rds/modify-backups.png)

## Restore from Automated Backup

Restoring from these backups is simple. Navigate to `RDS > Databases`, select the relevant database, and click the `Maintenance & backups` tab. Find the backup you wish to restore to at the bottom of the page, check the box next to it, and click on the `Restore` button.

More RDS snapshots, including any taken manually can also be under `RDS > Snapshots` but finding the relevant automated backup is much easier to do by navigating to the relevant RDS instance and finding the backup there.

## Manual Backups - Tableplus

There are some instances where a manual backup is required - for example you may need to import the latest data from a production database in to a QA environment. In these scenarios we can use Tableplus.

Database connection details can be found in 1Password. Once connected, open the relavent database and highlight the tables you wish you export. Click `File > Export` and select the `SQL` tab. With all boxes checked click `Export`.  Save the export to `GoogleDrive/Shared drives/383 Engineering/Dev Assets/MySQL Database Backups` using the following naming convention;

`dbname_yourname_yyyy-mm-dd_hh-mm-ss`

As an example;

`canvas-prod-vapor_Andy_2022-04-13_10-02-17`

To import the data back in to your database, open your database, select all of the tables, right-click and select `delete`. Check the box to `ignore foreign key checks`.

![ignore-foreign-checks](/Assets/backups-in-aws/rds/ignore-foreign-checks.png)

Commit your changes and refresh the database. Now click `File > Import > From SQL Dump`. Find, `Open` and `Import` your exported data.