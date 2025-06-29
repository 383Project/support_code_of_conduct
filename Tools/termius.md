[Table of Contents](/readme.md)

# SSH - Termius

In order to connect to the servers we use Termius to connect via SSH. Termius can be downloaded for Mac [here](https://termius.com/mac-os).

### Create a connection

You can find the connection details for the servers in 1password. If you need access to a server that you can't find in 1password then please speak to a 1password Admin as you may have not access to the relevant vault.

![1password](/Assets/1password.png)

Use these details to create a new SSH connection. In Termius click `Add > New Host` along the top and you will see the following appear down the right hand side.

![Termius](/Assets/Termius.png)

<B>Label:</B> The name for your server. This should be something that is recognisable to you, i.e. `383-project Prod`.
<B>Address:</B> IP Address for the server.
<B>Group:</B> Use groups to better organise if you have many servers saved.

<B>SSH</B>
<B>Username:</B> This will vary by OS of the server. AWS Linux AMI's will use `ec2-user`, Ubuntu instances will the username `ubuntu`.
<B>Password:</B> Leave blank. We use SSH Keys as opposed to Passwords.

Click `Set a Key > +New > Import from key file`. This will open Finder. Find the key specified in the 1Password entry. This will be saved in `Google Drive/Shared Drives/383 Engineering/KEYS`.

With the key now set you're ready to connect. All other fields can be left as their defaults.