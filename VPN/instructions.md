[Table of Contents](/readme.md)
    
# VPN Client management
383project uses OpenVPN running on EC2 servers in AWS. We must connect to the VPN to set our IP address for whitelisting purposes. This document is for use by DevOps to understand the infrasture for the VPN and will outline how we can simply and quickly create or remove users.

### VPN Infrastructure
The VPN uses two EC2 instances;
1. VPN_Host
2. VPN_CA

**VPN_Host** runs 24/7. This is the host that users will connect to and all traffic will go via the VPN_Host. This instance has an elastic IP address `18.168.159.76` that we can use for whitelisting access to our servers via SSH.
If for any reason this server breaks and has to be replaced we have snapshots of the instance that we can rebuild from. In this case it is important to reattach the elastic IP address to the new server and to ensure that the users list is up to date.

**VPN_CA** is a certificate authority used for signing certificates for new users to grant access to the VPN. This instance is to be <em>stopped</em> when not in use to reduce costs.

### Create a new user
To create a user for the VPN connect to the VPN_Host by SSH and simply run;

> ~/client-create

This will run a bash script that will automate the majority of an otherwise lengthy process.

You will be prompted to "Please enter a username". The format to use here is `FirstnameLastname`. For example: `JohnDoe`. Next you will be asked to confirm the Common Name. Leave this blank and just press <em>enter</em> to use the default common name.

The script will do the rest for you, booting up the VPN_CA, creating and signing a certificate and creating the relevant files on the VPN_Host.

Please update [this sheet](https://docs.google.com/spreadsheets/d/1SXSHKVeZZE2waOn9UOljqJKvEGFrQLBpRtVdnFufuTc/edit?usp=sharing) with the new user.

All that's left to do is to send the .ovpn file to the user. You can connect to the VPN_Host using [<em>Filezilla</em>](https://filezilla-project.org/download.php?platform=osx) to download the file and then email it to the user. A template email can be found [here](/EMAIL_TEMPLATE.md)
The file will be located in `~/client-configs/files`.

### Remove a user

When anyone leaves 383 we must revoke their access to the VPN. Similarly to creating a new client, you can run a bash script to simplify this process.

> ~/client-revoke

You will be prompted to "Please enter a username". You can verify the username on [this sheet](https://docs.google.com/spreadsheets/d/1SXSHKVeZZE2waOn9UOljqJKvEGFrQLBpRtVdnFufuTc/edit?usp=sharing).

All associated files will be deleted from both the VPN_Host and VPN_CA. Please also delete the user from the Google sheet.