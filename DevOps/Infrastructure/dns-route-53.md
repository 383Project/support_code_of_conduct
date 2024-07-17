# DNS - Route 53
[Table of Contents](/readme.md)

## What is Route 53?
Route 53 is a Domain Name System (DNS) web service. DNS is a system that translates domain names into IP addresses. It's like the phonebook of the internet, helping computers locate websites and other resources online. When you enter a domain name in your browser, DNS servers work behind the scenes to look up the corresponding IP address and route your request to the appropriate server. 

## Hosted Zones Setup
In order to use Route 53 we must first set up a hosted zone. A hosted zone is a container that holds information about how you want to route traffic for a domain, such as example.com, and its subdomains. In AWS, navigate to `Route 53 > Hosted zones` and `Create hosted zone`.

![Create hosted zone](/Assets/route-53/create-hosted-zone.png)

<b>Domain name:</b> This should be the main URL of the client site. 
<b>Description:</b> The domain name should be self-explanatory enough that a description should not be needed.
<b>Type:</b> If this is a public facing website - which it probably is - this should be set to `Public`. 
<b>Tags:</b> Are not needed.

## Adding Records
Navigate to `Route 53 > Hosted Zones` and select the URL for which you need to add DNS records. Click `Create record`.

![create-records](/Assets/route-53/create-record.png)
<b>Record name:</b> Depending on the records this may be very specific and you should consult instructions for the record set that you are applying for this. However, if this is an `A record` to point to a staging server for example then you may already know what you want this to be.
<b>Record type:</b> Is dependent on what you are trying to achieve. The drop down menu shows a short summary of what each records is used for.
<b>Value:</b> Depending on the records this may be very specific and you should consult instructions for the record set that you are applying for this. However, if this is an `A record` to point to a staging server for example then you may already know what you want this to be.
<b>TTL:</b> Time to Live. Controls how long each record is valid and how long it takes for record updates to reach your end users.
<b>Routing policy:</b> In most cases this is likely to be `Simple routing`.

At this point you can `Add another record` or if you have all the records that you wish to apply, `Create records`.

## Editing Records
In order to edit an existing record, navigate to `Route 53 > Hosted Zones` and select the URL for which you need to add DNS records. Click the check box for one record that you wish to edit and the details of that record will show on the right of the screen. From here you can click `Edit record`.

