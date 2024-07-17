[Table of Contents](/readme.md)

# SFTP - Filezilla

For the safe download of files from a server we can use SFTP. To make this simple we use FileZilla, which can be downloaded for Mac from [here](https://filezilla-project.org/download.php?platform=osx).

In order to connect to the servers we use Termius to connect via SSH. Termius can be downloaded for Mac [here](https://termius.com/mac-os).

### Create a connection

You can find the connection details for the servers in 1password. If you need access to a server that you can't find in 1password then please speak to a 1password Admin as you may have not access to the relevant vault.

![1password](/Assets/1password.png)

Use these details to create a new SFTP connection. In Filezilla open the `site manager`. You can either do this with the icon in the top left or by clicking on `File > Site Manager`.

![New Site](/Assets/new-site.png)

<b>Protocol:</b> Set this to `SFTP - SSH File Transfer Protocol`.
<b>Host:</b> IP Address of the server to which you will be connectting.
<b>Port:</b> Set this to `22`.
<b>Logon Type:</b> Set this to `Key File`.
<b>User:</b> Username as in the 1password entry. For AWS Linux AMI this is usually `ec2-user` or for an Ubuntu instance it is usually `ubunutu`.
<b>Key File:</b> Click `Browse` and locate the key file named in the 1password entry. This will be located in `Google Drive/Shared drives/383 - Engineering/KEYS`.

With the key now set you're ready to connect. Click `OK` to save the connection in your Site Manager or click `Connect` for a one time connection.