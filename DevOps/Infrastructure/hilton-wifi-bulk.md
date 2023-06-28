# Hilton WiFi Bulk Update Process
[Table of Contents](/readme.md)

## Prerequisites
Make sure you have downloaded the repository containing the required code. Docker should also be set up on your machine. If you haven't done this already, refer to the README file in the repository for detailed instructions on setting up Docker.

## Setting up the Environment
Open a terminal and navigate to the root directory of the downloaded repository. Create a symbolic link from the .env.local file to .env by running `ln -s .env.local .env` in the terminal.

## Database Setup
Connect to the local database using TablePlus. Verify that the required database schema is present. The name of the database schema can be found in the .env.local file within the codebase.

![.env.local](/Assets/wifi-bulk-update/env-local.png)

Export the production database as SQL one table at a time without compressing the files.

![export as SQL](/Assets/wifi-bulk-update/export-data.png)

Copy the exported database files to the /hilton-hotel-api/database/CSVs/SQL directory in the repository.

## Preparing CSV Data
Download a copy of the CSV file. This should be attached to the Jira ticket. If it is not then you'll need to contact the PM for the project.

Copy the downloaded CSV file to the /hilton-hotel-api/database/CSVs directory in the repository. This is done simply by dragging the file across from Finder in to the directory in VScode.

## Running the Update
In Docker, locate the Terminal running PHP within the hilton-hotel-api directory. navigate to `/var/www/hilton-wifi-admin/data/site` and run `php artisan db:seed --class=AmexTakeoverImport` in the Docker Terminal. This command initiates the bulk update process using the provided CSV data.

Wait for the process to complete. Upon successful completion, the necessary changes will be applied to the local database.

## Importing Updated Data to Staging
Once the previous step is finished, re-export all tables from the production database, excluding the `app_pb_page_builds` table. Combine the exported data into a single SQL file and compress it. Now you can import the compressed SQL file into the Staging schema of the database. This step ensures that the staging environment is updated with the latest data.

This is now ready for QA and once approved you'll need to run through all of the above steps again to ensure that the latest data is used from the SQL database. You can then import to the Production schema of the database at the end as opposed to Staging.