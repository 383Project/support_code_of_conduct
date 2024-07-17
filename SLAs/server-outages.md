[Table of Contents](/readme.md)
    
# Server Outage
In the event of a website going down there will be a notifiaction on the [Slack #uptime-alerts](https://team383.slack.com/archives/C02DU2UT81L) channel. The first thing we should do is to check that the site is actually down by visting the website in a browser. It's best to do this in a browser that you have not previously used for that site, or to clear your cache & cookies first. This ensures that you don't simply get a cached version of the site when in fact the site might be down.

Having verified that site is down the next step is to restart the Apache server. To do this, SSH in to the server using [Termius](../Tools/Termius). Now, depending on the OS the command to restart Apache may vary.

### AWS AMI Linux 2

Restart the apache service;
> sudo service httpd restart

Verify that apache is running;
> sudo service httpd status

### Ubuntu

Restart the apache service;
> sudo systemctl apache2 restart

Verify that apache is running;
> sudo systemctl apache2 status