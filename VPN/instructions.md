[Table of Contents](/readme.md)
    
# VPN Client management
383project uses the OpenVPN software running on an EC2 server. In order to connect to client servers we must do so via the VPN. We do this for whitelisting purposes to connect via SSH and reduce the need to administrate the security groups across a few dozen accounts.
We also provide access to the VPN to all staff and insist that they connect to the VPN whenever using public WiFi. This ensures that all data is encrypted in transit and helps to minimise risk of man-in-the-middle attacks and data scraping in public wifi areas.

Management of the VPN and it's clients is the sole responsibility of the Support Team.

## VPN Infrastructure
The VPN uses two EC2 instances;
1. VPN_Host
2. VPN_CA

**VPN_Host** runs 24/7. This is the server that users will connect to and all network traffic will go through. This instance has an elastic IP address `18.168.159.76` that we can use for whitelisting access to our servers via SSH.

If for any reason this server breaks and has to be replaced we have snapshots of the instance that we can rebuild from. In this case it is important to reattach the elastic IP address to the new server and to ensure that the users list is up to date. Check what users exist on the server at `~/client-configs/files` and recreate any users that are no longer on the server by following the instructions under <b>Create a new user</b> below.

**VPN_CA** is a certificate authority used for signing certificates for new users to grant access to the VPN. This instance is to be <em>stopped</em> when not in use to reduce costs. The `create-client` and `revoke-client` scripts will both give the option to shutdown the CA at the end and a cronjob has also been set up on `VPN_Host` to shutdown the CA at 6pm everyday if it's left switched on.

## Create a new user
To create a user for the VPN connect to the VPN_Host by SSH and simply run;

> ~/client-create

This will run a bash script that will automate the majority of an otherwise lengthy process.

You will be prompted to "Please enter a username". The format to use here is `FirstnameLastname`. For example: `JohnDoe`. Next you will be asked to confirm the Common Name. Leave this blank and just press <em>enter</em> to use the default common name.

The script will do the rest for you, booting up the VPN_CA, creating and signing a certificate and creating the relevant files on the VPN_Host.

Please update [this sheet](https://docs.google.com/spreadsheets/d/1SXSHKVeZZE2waOn9UOljqJKvEGFrQLBpRtVdnFufuTc/edit?usp=sharing) with the new user.

To download this file you can connect to the VPN_Host using [<em>Filezilla</em>](https://filezilla-project.org/download.php?platform=osx). Navigate to `~/client-configs/files` to download the file and test it on your own machine to verify it's working. Once verified, upload it to this [Google Drive folder](https://drive.google.com/drive/folders/1c0t145RwsqcKDt3YUvZbzA_6XN_15YWp?usp=share_link). From there, share the <em>individual file only</em> with the user. Instructions for using the file can be found [here](https://docs.google.com/document/d/13tg9fi3nFlA1rNCeyXnsj9U_212AjKj1xni7zQeUOr0/edit?usp=sharing).

## Remove a user

When anyone leaves 383 we must revoke their access to the VPN. Similarly to creating a new client, you can run a bash script to simplify this process.

> ~/client-revoke

You will be prompted to "Please enter a username". You can verify the username on [this sheet](https://docs.google.com/spreadsheets/d/1SXSHKVeZZE2waOn9UOljqJKvEGFrQLBpRtVdnFufuTc/edit?usp=sharing).

All associated files will be deleted from both the VPN_Host and VPN_CA. Please also delete update the user as `Revoked` in the [Google sheet](https://docs.google.com/spreadsheets/d/1SXSHKVeZZE2waOn9UOljqJKvEGFrQLBpRtVdnFufuTc/edit?usp=sharing) and move there .ovpn file from [AWS VPN Certs - Active](https://drive.google.com/drive/folders/1c0t145RwsqcKDt3YUvZbzA_6XN_15YWp?usp=sharing) to [AWS VPN Certs - Archived](https://drive.google.com/drive/folders/1ekGwWoyOrB3n0nC6KRra1Z6QW1Lm8NxU?usp=share_link).