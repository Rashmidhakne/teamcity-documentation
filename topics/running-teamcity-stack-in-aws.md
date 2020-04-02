[//]: # (title: Running TeamCity Stack in AWS)
[//]: # (auxiliary-id: Running TeamCity Stack in AWS)

You can run the TeamCity stack in AWS using the [CloudFormation template](https://github.com/JetBrains/teamcity-cloudformation-template). Note that this is an experimental option, which is currently in progress.

## Stack Overview

The current setup uses 2 subnets, a public and a private one.
* The private subnet includes all the essential items:
  * ECS cluster of a CoreOS EC2 instance with the official TeamCity server of the specified version from Docker Hub and one TeamCity Build Agent. The official Docker images with the TeamCity server and build agent are used.
  * RDS MySQL database
* The public subnet includes:
  * Application Load Balancer
  * NAT gateway ensuring the publicly available IPs

Both subnets are placed into a Virtual Private Cloud (VPC) which is completely secure. The database allows only internal connections within the VPC and its possible to connect to the Server via HTTP(s) or SSH only.

## Prerequisites

To create a TeamCity stack and connect to it, you will need:
* [EC2 KeyPair](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-key-pairs.html) in the same region as the TeamCity stack
* Installed SSH client to connect to the TeamCity server and view the logs
* IAM permissions to create the service\-linked role and apply a policy to it for the IAM entity creating the stack

## Using Template

1\.  On the _Select Template_ page, select the default TeamCity Template and click __Next__.

2\.  Specify the stack name and parameters provided by the template:

### Template Parameters

<seealso>
        <category ref="blog">
            <a href="https://blog.jetbrains.com/teamcity/2017/10/teamcity-aws/">Official TeamCity CloudFormation template</a>
        </category>
</seealso>
