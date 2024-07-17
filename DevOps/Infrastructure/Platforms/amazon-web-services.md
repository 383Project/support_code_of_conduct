# Amazon Web Services
[Table of Contents](/readme.md)
- [Amazon Web Services](./amazon-web-services.md)
- [Rackspace](./rackspace.md)

## What is AWS?
AWS is a hosting solution where Amazon manages and administrates a magantude of different services ranging from typical blade style servers to Content Delivery Networks, massive storage solutions and serverless technologies. This suite of technologies is commonly referred to as "The Cloud".

## Why we use AWS
AWS provides a large range of technical solutions and it's suite is ever increasing in scope and scale, however AWS' biggest strength in it's ability to be plugged into other technical solutions via it's API.

Utilising AWS' API we've been able to create the [AWS Server Tracker](https://docs.google.com/spreadsheets/d/1MM4LabigHVVRLJmt-97n4RoL7gYdkUGy3dFZiN1iIM8/edit#gid=0). By using Google's Sheets and Scripts, we are able to check on the status of servers in real time, and monitor the costs incurred on the various accounts we manage. Additionally using a webhook for Slack integration, we're able to configure alerts notifying specific individuals of server faults, predicted costs exceeding expectations, and other quantifiable checks utilising data from AWS' API.

## How we use AWS
Initially we setup a separate accounts for the client/project under the [root 383 account](https://start.1password.com/open/i?a=YZCR7KAOAFA57KI3ZTNJ6VOQWI&v=2a6iq66k7eaczk3su5tw3oi724&i=5up4dhresrgr5ptzvsl75b67im&h=team383.1password.com). In the future, this can also be done using the AWS Server Tracker by feeding it a JSON object dictating the infrastructure that needs to be setup.

Once the account has been created the details been to be added to the appropriate 1password vault, this should be `<Client Name> - DevOps`. This vault should be fully accessible by Fiance and DevOps, with special exception allowing access to specific individuals on a case by case basis.

After the [Choosing of Infrastructure](../choosing-infrastructure.md) phase of the project development, a clear list of requirements for the infrastucture should be established allowing the Support Team to begin setting up the services needed. If the tech stack doesn't require serverless then the [Basic EC2 Setup 2021](https://docs.google.com/document/d/1f09U_rCC9sXAYNvQwMYRutzStEOfuqB0rq9ASzX-pyk/edit) should surfice in setting up the infrastructure.