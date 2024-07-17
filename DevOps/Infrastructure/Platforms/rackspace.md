# Rackspace
[Table of Contents](/readme.md)
- [Amazon Web Services](./amazon-web-services.md)
- [Rackspace](./rackspace.md)

Rackspace is a service that's used primarily for legacy projects/systems only, there are two main accounts [apps383](https://start.1password.com/open/i?a=YZCR7KAOAFA57KI3ZTNJ6VOQWI&v=6m3d5rt7rmtcvn4pthnhl2jtne&i=poetamjvyjdtpopnsh33btuj44&h=team383.1password.com) and [hiltonwifi383](https://start.1password.com/open/i?a=YZCR7KAOAFA57KI3ZTNJ6VOQWI&v=6m3d5rt7rmtcvn4pthnhl2jtne&i=je3zcrhiurfjlfblp2pnhjy5oa&h=team383.1password.com).

## Cloud DNS
Few of our projects require the Cloud DNS service of Rackspace, however one in particular is hiltonapps.com. All the DNS records for hiltonapps.com can be found in the [apps383](https://start.1password.com/open/i?a=YZCR7KAOAFA57KI3ZTNJ6VOQWI&v=6m3d5rt7rmtcvn4pthnhl2jtne&i=poetamjvyjdtpopnsh33btuj44&h=team383.1password.com) account. If you wish to modify an existing record or create additional records it must be done on this account.

## SSL Certificates
### Creation of CSRs
In order to create a new SSL certificate for any servers hosted on any of the Rackspace accounts the following information needs to be provided:
- Common Name:
- Organization:
- Organization Unit:
- City/Locality:
- State/Province:
- Country/Region:
- Bit Length: `2048`

Bit Length is the only value with a default value of `2048`, all the other details must be provided in order to generate the Certificate Signing Request (CSR). All other details should be provided with the JIRA ticket to update the SSL certificate.

*Note: Common Name is used to enter the value of the domain name.*

### Keys
In order to create a CSR a key needs to be provided. These keys can be generated dynamically as part of the creation of the CSRs or an existing one can be used instead. **It is important that all keys are kept safe.** Even though it's not critical, keys should be generated for each CSR and used only once.

### Requesting the SSL Certificate
Once the CSR has been generated, it needs to be attached to the original JIRA ticket along with the key used to generate the CSR. Both will need to be provided when installing the SSL certificate on AWS or Rackspace.

Once the ticket has been updated the Project Manager in charge of getting the SSL certificate from the client will need to contact them providing the CSR. Once the client has provided the SSL certificate it can now be installed on the server.

### Installing an SSL certificate on Rackspace
All Rackspace servers are setup with a Load Balancer, this is where the SSL certificate needs to be installed.

When you come to the Rackspace Load Balancers screen you're greeted with a series of Load Balancers by name and IP Address. To verify the correct Load Balancer, ping the domain name that was used in the Common Name to obtain the IP Address of the server. Once you have that you'll be able to determine the Load Balancer that the SSL certificate is fore.

Once in the Load Balancer you'll find need to scroll down until you find the section called `Secure Traffic (SSL)` and near it a pencil icon denoting that it can be edited.

From there you can update the content of the SSL with the body of the SSL certificate, the CSR, and the Key.

## Cloud Servers
Rackspace Cloud Servers are typical

## Load Balancers

### Communication between Load Balancer and Server over port 80