# Load Balancers in AWS
[Table of Contents](/readme.md)

## What Are Load Balancers?
Load balancers help to distribute incoming network traffic across multiple servers, making sure that no single server gets overwhelmed with too much traffic. They work by monitoring the traffic coming into a server and then distributing it to different servers based on factors like server availability, capacity, and performance. Load balancers are commonly used in high-traffic websites or applications that require high availability and scalability. They can improve the overall performance and reliability of the application, by ensuring that no single server gets overloaded with traffic causing a bottleneck.

## How To Set Up Load Balancers In AWS to have an IP address.

### Target Groups

There's a few things we need to do in order to set up a load balancer to have an IP address. We first need to setup an application load balancer, and then a network load balancer. However, before we set up a load balancer we first need to set up a target group for the load balancer to use.

To do this, navigate to the `EC2 dashboard`. Click on `Target Groups` in the left-hand menu and then `Create target group`.

![create-target-group](/Assets/load-balancers-in-aws/target-group.png)
<b>Target type:</b> Set to `Instances`.
<b>Target group name:</b> This should be something sensible that relates to the project such as `prod-client-target-group`
<b>Protocol:</b> HTTP on port 8
<b>VPC:</b> Needs to be the same VPC that your instances are on.
<b>Protocol version:</b> HTTP1
<b>Health check prototcol:</b> HTTP.
Everything else can be left as default
Click on `next`.

![seclect-targets](/Assets/load-balancers-in-aws/select-targets.png)
On the next screen you'll need to select the servers to be included in your load balancer. Click the check boxes and `Include as pending below`. You'll see the instances added to the targets for review. Once you have checked that these are correct `create target group`.

### Application Load Balancer

Now we can create our first load balancer, starting with an application load balancer. On the left of the screen navigate to `Load balancers` and click `Create load balancer` followed by `Application load balanacer`.

<b>Load balancer name:</b> This should be something sensible that relates to the project followed by alb for application load balancer, such as `prod-client-alb`
<b>Sheme:</b> It's recommended to use `internet-facing` for testing purposes.
<b>IP address type:</b> IPv4 
<b>VPC:</b> Needs to be the same VPC that your instances are on.
<b>Mappings:</b> This is not too important but if you open another tab and navigate to `ec2 > instances` you can see the availability zones of your instances and use two of the same AZ's. There may be additional cost implications for using more than 2 AZ's.
<b>Security groups:</b> Remove the default security group and apply <em>only</em> the `http-public` security group.

Give your target group a name, protocol, and port number.
Select the VPC that you want to associate with the target group.
Choose the type of target, either instance or IP address.
Select the instances or IP addresses to include in the target group.
Review and create the target group.
Once you have created the target group, you can attach it to your load balancer. To do this, navigate to the "Load Balancers" section in the EC2 dashboard, select your load balancer, and then click the "Listeners" tab. From there, you can add the target group to your load balancer and specify the routing rules for incoming traffic. This allows you to distribute incoming traffic to the appropriate target groups based on criteria like port, protocol, and health status.