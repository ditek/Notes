# AWS
<!-- MarkdownTOC -->

- [Definitions](#definitions)
- [RDS](#rds)
    - [Configuring with public access](#configuring-with-public-access)
    - [RDS Autoscaling](#rds-autoscaling)
    - [RDS High Availability](#rds-high-availability)
- [S3](#s3)
    - [CORS](#cors)
    - [Hosting static websites](#hosting-static-websites)
    - [Objects Access](#objects-access)
- [EC2](#ec2)
    - [Instance Store](#instance-store)
    - [EBS](#ebs)
    - [Bastion Hosts](#bastion-hosts)
    - [Launch Templates](#launch-templates)
    - [Load Balancers](#load-balancers)
    - [Auto Scaling](#auto-scaling)
- [VPC](#vpc)
    - [Subnets](#subnets)
        - [Public Subnets](#public-subnets)
        - [Private Subnets](#private-subnets)
    - [Internet Gateway](#internet-gateway)
    - [NAT Gateway](#nat-gateway)
    - [Route tables](#route-tables)
    - [Elastic Network Interfaces](#elastic-network-interfaces)
    - [Elastic IP address](#elastic-ip-address)
    - [Connecting VPCs](#connecting-vpcs)
        - [VPC Peering](#vpc-peering)
        - [Transit Gateway](#transit-gateway)
        - [Interface Endpoint](#interface-endpoint)
- [ELB](#elb)
- [VGW \(Virtual Private Gateway\)](#vgw-virtual-private-gateway)
- [DX \(AWS Direct Connect\)](#dx-aws-direct-connect)
- [Security](#security)
    - [IAM](#iam)
        - [Naming Conventions](#naming-conventions)
        - [Policy Files](#policy-files)
            - [Actions Examples](#actions-examples)
            - [Resource Examples](#resource-examples)
        - [Installing AWS User IAM Profiles Locally](#installing-aws-user-iam-profiles-locally)
        - [IAM Service Roles](#iam-service-roles)
        - [Permissions for working with ElasticBeanstalk](#permissions-for-working-with-elasticbeanstalk)
    - [Security Groups](#security-groups)
    - [ACL](#acl)
- [Elastic Beanstalk](#elastic-beanstalk)
    - [EB CLI](#eb-cli)
        - [Deploying to EB](#deploying-to-eb)
    - [Autoscaling](#autoscaling)
- [Lambda](#lambda)
    - [Lambda Structure](#lambda-structure)
    - [Handler TypeScript Types](#handler-typescript-types)
    - [Invoke from CLI](#invoke-from-cli)
    - [Uploading Code](#uploading-code)
    - [Lambda logs in CloudWatch](#lambda-logs-in-cloudwatch)
    - [Configuring Trigger](#configuring-trigger)
    - [API Gateway](#api-gateway)
        - [Endpoint Types](#endpoint-types)
        - [Stages](#stages)
        - [CORS](#cors-1)
        - [Request Validation](#request-validation)
    - [WebSocket API](#websocket-api)
        - [Routing WebSocket Traffic to Lambdas](#routing-websocket-traffic-to-lambdas)
        - [Interacting with Connections](#interacting-with-connections)
    - [Custom Authorizers](#custom-authorizers)
- [Databases](#databases)
    - [DynamoDB](#dynamodb)
        - [Scan](#scan)
        - [Query](#query)
        - [Composite key](#composite-key)
        - [Primary key](#primary-key)
        - [Index Types](#index-types)
        - [Update Stream](#update-stream)
        - [NoSQL Data Modelling](#nosql-data-modelling)
        - [Local DynamoDB instance](#local-dynamodb-instance)
- [CloudFormation](#cloudformation)
    - [Resource References](#resource-references)
    - [Multi-layer Infrastrucure](#multi-layer-infrastrucure)
- [Kinesis](#kinesis)
- [Simple Notification Service \(SNS\)](#simple-notification-service-sns)
- [Key Management Service \(KMS\)](#key-management-service-kms)
- [AWS Secret Manager](#aws-secret-manager)
- [Systems Manager Parameter Store \(SSM\)](#systems-manager-parameter-store-ssm)
- [Labs](#labs)
    - [IAM](#iam-1)
    - [Auto Scaling](#auto-scaling-1)
    - [Cloud Watch](#cloud-watch)
- [AWS CLI](#aws-cli)
    - [Config](#config)
- [Certification](#certification)
- [Resources](#resources)

<!-- /MarkdownTOC -->

# Definitions
Elastic Block Store

**Elastic Block Store (EBS)** is a storage solution for EC2 instances and is a physical hard drive that is attached to the EC2 instance to increase storage. EBS 
- persist data after instance terminated.
- Automatically replicated within its Availability Zone

**Elastic Beanstalk** is an orchestration service that allows you to deploy a web application at the touch of a button by spinning up (or provisioning) all of the services that you need to run your application.

**Relational Database Service (RDS)**

**Redshift**: a cloud data warehousing service to help companies manage big data. Redshift allows you to run fast queries against your data using SQL, ETL, and BI tools. Redshift stores data in a column format to aid in fast querying.

**CloudFront** is used as a global content delivery network (CDN). Cloud Front speeds up the delivery of your content through Amazon's worldwide network of mini-data centers called Edge Locations.

**Identity & Access Management (IAM)** is an AWS service that allows us to configure who can access our resources.

**Route 53** is a cloud domain name system (DNS). It allows you to route users based on the user’s geographic location.

**Simple Notification Service (SNS)** is a cloud service that allows you to send notifications to the users of your applications.
- SNS uses a publish/subscribe model.
- SNS can publish messages to Amazon SQS queues, AWS Lambda functions, and HTTP/S webhooks.

**Simple Queue Service (SQS)** is a fully managed message queuing service that allows you to integrate queuing functionality in your application. SQS offers two types of message queues: standard and FIFO.
- FIFO queues guarantee the ordering of messages.
- Standard queues offer best-effort ordering but no guarantees. They deliver a message at least once.

**Elastic Container Service (ECS)** is an orchestration service used for automating deployment, scaling, and managing of your containerized applications.

**Cloud Trail** allows you to audit (or review) everything that occurs in your AWS account. Cloud Trail does this by recording all the AWS API calls occurring in your account and delivering a log file to you. 

**Cloud Watch** is a service that monitors resources and applications that run on AWS by collecting data in the form of logs, metrics, and events. 

**Cloud Formation** allows you to model your entire infrastructure in a text file template allowing you to provision AWS resources based on the scripts you write. Templates are written using JSON or YAML.

**Signed URLs** allow clients to send and receive data by directly communicating with the file store. This saves the server from using its bandwidth to serve as the intermediary that transmits data to and from the client.

**CloudFront** is a content delivery network offered by Amazon Web Services.

# RDS

## Configuring with public access
RDS Postgres setup:
- https://www.youtube.com/watch?v=2ydzbZjoB-Q
- https://www.youtube.com/watch?v=JEh35M7LGbo

Configuring public access:
- https://www.youtube.com/watch?v=4PnjHumSNA0
- From VPC service, create a security group.
- Edit security group's inboud rules: Type=PostgreSQL, Source=Anywhere
- Modify RDS to use the new security group and change `Publicly accessible` to `Yes`.

## RDS Autoscaling
https://aws.amazon.com/blogs/database/scaling-your-amazon-rds-instance-vertically-and-horizontally/

## RDS High Availability
From the DB's settings, for Multi-AZ deployment, select `Create a standby instance`.

___
# S3
S3 has a flat structure. If you place a file in a directory, it actually just adds a _prefix_ to the file name.

## CORS
CORS (Cross Origin Resource Sharing) defines how a client can interact with a resource, and what the client can and cannot do with that resource.

This policy allows REST connections from any client:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<CORSConfiguration xmlns="http://s3.amazonaws.com/doc/2006-03-01/">
<CORSRule>
    <AllowedOrigin>*</AllowedOrigin>
    <AllowedMethod>POST</AllowedMethod>
    <AllowedMethod>GET</AllowedMethod>
    <AllowedMethod>PUT</AllowedMethod>
    <AllowedMethod>DELETE</AllowedMethod>
    <AllowedMethod>HEAD</AllowedMethod>
    <AllowedHeader>*</AllowedHeader>
</CORSRule>
</CORSConfiguration>
```

## Hosting static websites
https://aws.amazon.com/premiumsupport/knowledge-center/cloudfront-serve-static-website/

## Objects Access
Objects are private by default. To make them public:
- Use a _bucket policy_ to make an entire bucket or ajust a directory public.
- Use an _access control list (ACL)_ to make indivicual objects public.

___
# EC2

_Architecture Tip_
Store session information outside the server in Elastic Cache with Reddis or DynamoDB.

## Instance Store
Physical storage connected directly to the instance.j
Not persistent.

## EBS
EBS provides storage connected to EC2 over the network and it is persistent even if the EC2 instance attached to it is stopped.
- If EBS is used for boot, it will be (by default) removed when EC2 is removed.
- If EBS is used for extra storage, it will not be (by default) removed when EC2 is removed.

Sharing data between EC2 instances:
- For WORM (Write Once Read Many) usecases, S3 is suitable for sharing data.

EC2 plans:
- Compute savings plan.
- Spot instances: Save up to 90%, but it can be taken at any time. Use we you need the capacity, but don't care if some instance live an die dynamically.

## Bastion Hosts
A jump host that is used to SSH into EC2 instances.

## Launch Templates
You can create a launch template that includes the parameters required to launch an EC2 instance, such as the ID of the Amazon Machine Image (AMI) and an instance type. The next time, we can just create EC2 instance from a launch template instead of specifying the parameters.

## Load Balancers
When your application is running on multiple application servers, you need a way to distribute traffic among those servers. You can accomplish this by using a load balancer. A load balancer distributes incoming application traffic across multiple instances. A load balancer also performs health checks on instances and only sends requests to healthy instances.

Creation steps:
- EC2 -> Load Balancers -> Create.
- Under `Availability Zones`, select the subnets where the instances are located.
- Configure or add a security group that would allow the required traffic.
- We can optionally configure routing to route different traffic to different targets based on endpoint for example.
- We can attach an auto scaling group once we create it.

## Auto Scaling
Amazon EC2 Auto Scaling is a service designed to launch or terminate Amazon EC2 instances automatically based on user-defined policies, schedules, and health checks. The service also automatically distributes instances across multiple Availability Zones to make applications highly available.

To perform auto scaling, we need to create an auto scaling group. Auto Scaling groups are collections of Amazon EC2 instances that enable automatic scaling and fleet management features. 

An auto scaling group should span all AZs in the region.

Creation steps:
- EC2 -> Auto Scaling Groups -> Create.
- Choose a launch template.
- Choose `Attach to an existing load balancer` if relevant.
- Check `Enable group metrics collection within CloudWatch`.


___
# VPC
VPC is a regional network that can have multiple subnets, each with a subset of the VPC's CIDR block. Every subnet is limited to one AZ.
- AWS reserves five addresses from each subnet.
- We don't launch resources directly in the VPC, but rather in the subnets.

DNS can be enabled for the VPC to add a friendly name when using it. Any Amazon EC2 instances launched into the VPC will automatically receive a DNS hostname. To enable it:
- Actions -> Edit DNS hostnames -> Enable.

## Subnets
A subnet is a sub-range of IP addresses within the VPC. You can launch AWS resources into a specified subnet. Use a public subnet for resources that must be connected to the internet, and use a private subnet for resources that are to remain isolated from the internet.

How to add public access to a subnet:
- Add one Internet Gateway per VPC.
- If the private subnet needs to access the internet, add a NAT Gateway to the public subnet and connect it to the private subnet.

_Architecture Tip:_
Subnet design recommendation:
- One public (if needed) and one private per AZ. (exception: resources which require absolutely no access to the internet, either directly or indirectly, would go into a separate private subnet)
- Prefer few large subnets to many small subnets(/24 and larger).
- Use larger private subnets (/23) and smaller public subnets (/24).

_Architecture Tip:_
Rather than define your subnets based on application or functional tier (web/app/data/etc.), you should organize your subnets based on internet accessibility. This allows you to define clear, subnet-level isolation between public and private resources.

_Architecture Tip:_ 
While you can put web-tier instances into a public subnet, AWS recommends that you put web-tier instances inside private subnets behind a load balancer placed in a public subnet.

### Public Subnets
If a subnet is associated with a route table that has a route to an internet gateway, it is known as a public subnet.

A public subnet must have an internet gateway.

To create a public subnet:

    - Select the subnet -> Actions -> Modify auto-assign public IPv4 address -> Enable auto-assign public IPv4 address.
    - Create an internet gateway and attach to the VPC.
    - Create a route table.
    - Add a route to the route table that directs 0.0.0.0/0 traffic to the internet gateway.
    - Associate the route table with the subnet, which therefore becomes a public subnet

### Private Subnets
- Do not have a routing table entry to an internet gateway.
- Are not directly accisble from the public internet.
- Typically use a NAT gateway to support restricted, outbound public internet access. 

## Internet Gateway
An internet gateway is a horizontally scaled, redundant, and highly available VPC component that allows communication between instances in a VPC and the internet. An internet gateway does not impose availability risks or bandwidth constraints on network traffic.

An internet gateway serves two purposes:

- To provide a target in route tables to connect to the internet.
- To perform network address translation (NAT) for instances that have been assigned public IPv4 addresses.

Creation:
- From VPC -> Internet Gateways -> Create.
- After creation: Actions -> Attach VPC.
- configure the route table of the public subnet to use the internet gateway.

## NAT Gateway
Enables instances in the private subnet to initiate outbound traffic to the internet or other AWS services.
- Prevents private instances from receiving inbound traffic from the internet.

## Route tables
A route table contains a set of rules, called routes, which are used to determine where network traffic is directed. Each subnet in a VPC must be associated with a route table; the table controls the routing for the subnet. A subnet can only be associated with one route table at a time, but you can associate multiple subnets with the same route table.

When you create a VPC, it automatically has a main route table, which, initially, contains only a single route: a local route that enables communication for all the resources within the VPC. If you don't explicitly associate a subnet with a particular route table, the subnet is implicitly associated with and uses the main route table.

To use an internet gateway, a subnet's route table must contain a route that directs internet-bound traffic to the internet gateway. If a subnet is associated with a route table that has a route to an internet gateway, it is known as a public subnet.

Public route table:
- Edit routes -> Add route -> Set destination to `0.0.0.0/0` and Target to the Internet Gateway created earlier.
- Associate the route table with the public subnet:
  + Subnet Associations -> Edit Subnet Associations -> Choose the public subnet.

__Example__:

Public route table              Private route table

Destination | Target            Destination | Target
--------------------            --------------------
10.0.0.0/16   local             10.0.0.0/16   local
0.0.0.0/0     <igw-id>          0.0.0.0/0     <nat-id>

## Elastic Network Interfaces
An elastic network interface is a virtual network interface that you can attach to an instance in a VPC. You can create a network interface, attach it to an instance, detach it from an instance, and attach it to another instance. The attributes of a network interface, including the private IP address, elastic IP address, and MAC address, follow the network interface, because it is attached to or detached from an instance and reattached to another instance.

## Elastic IP address
An Elastic IP address is a static, public IPv4 address designed for dynamic cloud computing. You can associate an Elastic IP address with any instance or network interface for any VPC.

## Connecting VPCs

### VPC Peering
A VPC peering connection is a networking connection between two VPCs that enables you to route traffic between them privately. Instances in either VPC can communicate with each other as if they are within the same network. You can create a VPC peering connection between your own VPCs, with a VPC in another AWS account, or with a VPC in a different AWS Region.

*Notes from slides*
Not single point of failure. Connection is managed by AWS and highly available.
Not very scalable. One VPC can connect up to 125 VPCs.

Steps for peering:
- Create a new Peering Connection and accept it.
- Update the route tables in both VPCs to send traffic that belongs to the IP range of the other VPC to the peering connection.

### Transit Gateway
Up to 5000 VPC connections.


### Interface Endpoint
Allows connecting to AWS services or VPC without going thourhg the internet.
- Not bidirectional. Requests have to be initiated from the client tot he server.

___
# ELB
- Addressed via DNS name.
- Can be facing the internet of internal services.

___
# VGW (Virtual Private Gateway)

Max BW is 1.25Gbps


# DX (AWS Direct Connect)
A dedicated private connection to AWS.
Usually used to connect on prem data centers to AWS og transferring a lot of data from AWS.

___
# Security

## IAM
It's recommended to add users to a group so users/service with similar needs can simply be assigned to that group. A group can have multiple policies.

A policy defines the AWS permissions that you can assign to a user, group, or role for accessing a specific service, e.g. S3 or EC2.

Steps for creating a user, a group and a policy:
- https://www.youtube.com/watch?v=DJ0wYhp_-cc

Once a user is created, you will be given a `credentials.csv` file, which should be saved.

### Naming Conventions
Users:
- It is recommended to have different users for development and production environments, even if you work alone.
- User name example: 

### Policy Files
Policy JSON file have the following structure:

```json
{
    // A list of permissions in this policy
    "Statement": [
        {
            "Effect": "Allow",
            // One action or a list of actions
            "Action": [
                "ec2:TerminateInstance"
            ],
            // Resources ARN this applies to (e.g. an EC2 instance). Can be a list
            "Resource": "*"
        }
    ]
}
```

#### Actions Examples
```yaml
// EC2
ec2:TerminateInstance

// DynamoDB
Action:
  - dynamodb:Scan
  - dynamodb:PutItem
  - dynamodb:GetItem
  - dynamodb:DeleteItem
  - dynamodb:Query
  - dynamodb:UpdateItem
Resource: arn:aws:dynamodb:${self:provider.region}:*:table/${self:provider.environment.MY_TABLE}

// S3
Action:
  - s3:PutObject
  - s3:GetObject
Resource: arn:aws:s3:::${self:provider.environment.MY_BUCKET}/*
```

#### Resource Examples
```js
"arn:aws:dynamodb:us-east-1:*:table/MyTable"
```

### Installing AWS User IAM Profiles Locally
Using the command

```sh
aws configure
```

You will be asked for the user credentials. Use the file provided when the user was created. The credentials will be added to `~/.aws` under `default` profile. Other profiles can be created when multiple users need to be configured.

```sh
# ~/.aws/credentials
[default]
aws_access_key_id=########################
aws_secret_access_key=########################
[profile1]
aws_access_key_id=########################
aws_secret_access_key=########################

# ~/.aws/config
[default]
region=us-east-1
[profile1]
region=us-west-2
```

### IAM Service Roles
For services that need to access resources, we need to create roles. Roles can apply to EC2 instances or lambdas.

### Permissions for working with ElasticBeanstalk
We add `AWSElasticBeanstalkFullAccess` 

___
## Security Groups
A security group acts as a virtual firewall for instances to control inbound and outbound traffic. Security groups operate at the instance network interface level, not the subnet level. Therefore, each instance can have its own firewall that controls traffic. If you do not specify a particular security group at launch time, the instance is automatically assigned to the _default security group_ for the VPC. By default, security groups allow no inbound traffic and all outbound traffic.

A security group acts as a virtual firewall that controls the traffic for one or more instances. When you launch an instance, you associate one or more security groups with the instance. You add _rules_ to each security group, and these rules allow traffic to or from the group's associated instances. You can modify the rules for a security group at any time; the new rules are automatically applied to all instances that are associated with the security group.

When you created the inbound rule for the Database Security Group, notice that you used the Application Security Group ID as the source. The ability for one security group to refer to another security group is a powerful capability. It means that you can grant additional EC2 instances to have access to the database by associating them with the Application Security Group. Any instance associated with the Application Security Group will then be permitted to communicate to the database (more accurately, to any database associated with the Database Security Group).

Security groups are stateful, meaning that if a request is allowed in the inbound rules, its response will be allowed even if it's not explicitly allowed in the outbound rules.

An inbound rule can point to another security group to automatically take its outbound rules.

Naming:
- For example `App-SG`

___
## ACL
ACLs are stateless, so unlike security groups, if a request is allowed in the inbound rules, its response will _not_ be allowed if it's not explicitly allowed in the outbound rules.

The rule with the highest number is evaluated first.

___
# Elastic Beanstalk

## EB CLI
- Install EB CLI
- Run `eb init` in you project directory to create a new appliation.
- Create a new ssh keypair or use an existing one.
- A file `.elasticbeanstalk/config.yml` will be created at the project root.

### Deploying to EB
EB expects to deploy a zipped archive of JS files. We specify the archive directory in `.elasticbeanstalk/config.yml`:

```yaml
deploy:
    artifact: ./www/Archive.zip
```

Then we add the following scripts to our `package.json`:

```json
"scripts": {
"start": "node .",
"tsc": "tsc",
"dev": "ts-node-dev --respawn --transpileOnly ./src/server.ts",
"prod": "tsc && node ./www/server.js",
"clean": "rm -rf www/ || true",
"build": "npm run clean && tsc && cp -rf src/config www/config && cp .npmrc www/.npmrc && cp package.json www/package.json && cd www && zip -r Archive.zip . && cd ..",
"test": "echo \"Error: no test specified\" && exit 1"
},
```

Running `npm run build` should transpile our code and create `./www/Archive.zip`

Now we need to create an environment.
- Run `eb create`
- Choose an environment name and load balancer (`application` for example)
- The code should be deployed to S3

## Autoscaling
https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/environments-cfg-autoscaling-triggers.html

_______________________________________________________________________________
# Lambda

## Lambda Structure

```js
exports.handler = async (event, context, callback) => {
    return {
        statusCode: 200,
        // Allow CORS
        headers: {
          'Access-Control-Allow-Origin': '*'
        },
        body: "A string body"
    }
};
```

- `event`: is the event object that triggered the lambda. Usually a JSON object.
    + `queryStringParameters`: like `id` in `/user?id=1`. It can be undefined.
    + `pathParameters`: in `/users/{id}` accessing `/user/1` will give `id=1`.
- `context`: Information about the execution environment. Contains several fields:
    + `functionName`
    + `functionVersion`
    + `memoryLimitInMB`
    + `logGroupName`
    + `logStreamName`
    + `getRemainingTimeInMillis()`
- `callback`: Can be optionally used to return an error or result from the function. Useful if not using async/await.

## Handler TypeScript Types
```js
export const handler: SNSHandler = async (event: SNSEvent) => {}
export const handler: APIGatewayProxyHandler = async (event: APIGatewayProxyEvent): Promise<APIGatewayProxyResult> => {}
export const handler: DynamoDBStreamHandler = async (event: DynamoDBStreamEvent) => {}
```

## Invoke from CLI

```sh
# RequestResponse event
aws lambda invoke --function-name my-function \
    --invocation-type RequestResponse \
    --log-type tail \
    --payload '{"name": "My Event"}' \
    result.txt
```

Invocation types:
- `RequestResponse`: The result of completing the function is returned
- `Event`: The function is invoked asynchronously and we get error code 202 if the invocation request is received. AWS will try to run the function 3 times. If that fails, the event is stored into a Dead-Letter Queue.

## Uploading Code
If our function need dependencies and other files, we can create the project locally, zip it, and uploaded it to lambda.

```sh
zip -r my-project.zip .
```

## Lambda logs in CloudWatch
CloudWatch can be used to view logs and create events to pass our lambda function. We simply create a new rule and select our lambda as a target.

## Configuring Trigger
A lambda trigger can either be configured from the lambda settings (Add trigger) or from the resource (e.g. `Create event notification` from an S3 bucket settings).

_______________________________________________________________________________
## API Gateway
Enables creating and deploying REST and WebSocket APIs.

### Endpoint Types
- Edge optimized: Requests go through CloudFront first which chooses the best path to send it to the gateway. Suitable for cases where users are spread around the world.
- Regional: Request go directly to the gateway. Suitable if most users are in one region.

### Stages
Stages are snapshots of the API. For example, you can have a production stage and a development stages which use different API versions.

### CORS
API Gateway provides CORS support that would add an OPTIONS method to the API and populate it with the headers needed. To enable it, you only need to click `Actions -> Enable CORS`.

### Request Validation
It allows defining a JSON model to validate incoming objects in the requests.

```json
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "title": "my-type",
  "type": "object",
  "properties": {
    "name": {
      "type": "string"
    },
    "id": {
      "type": "number"
    }
  },
  "required": ["id"],
  // Whether additional fields are allowed
  "additionalProperties": false
}
```

_______________________________________________________________________________
## WebSocket API
WebSocket API provides two URLs:

- WebSocket URL:
    + Clients will use to connect to the API
    + Allows clients to send messages and receive notifications
- Connection URL
    + Send a message back to a connected client
    + Lambda function will use to send messages
    + Requires a connection id to send a message to a particular client. The id is sent by API Gateway upon connection or disconnection.

Connection URL supports the following operations:
- POST: to send a message to a client
- GET: to get the latest connection status
- DELETE: to disconnect a client from API


### Routing WebSocket Traffic to Lambdas
We can specify a field in the JSON payload that can function as a routing key. For example, `{"event": "send_message"}` would trigger a specific function.

There are also predefined special routes:
- `$connect` - sent when a user connects.
- `$disconnect` - sent when a user disconnects.
- `$default` - sent when no other when a message does not match any other route or when it has non-JSON payload.

### Interacting with Connections

```js
const connectionParams = {
  apiVersion: "2018-11-29",
  endpoint: `${apiId}.execute-api.us-east-1.amazonaws.com/${stage}`
}
const apiGateway = new AWS.ApiGatewayManagementApi(connectionParams)

export const handler: APIGatewayProxyHandler = async (event: APIGatewayProxyEvent): Promise<APIGatewayProxyResult> => {
  const connectionId = event.requestContext.connectionId;
  await sendMessage(connectionId, "hello")
}

async function sendMessage(connectionId, payload) {
    try {
        await apiGateway.postToConnection({
            ConnectionId: connectionId,
            Data: JSON.stringify(payload)
        }).promise()
    } catch (e) {
        if (e.statusCode == 410) {
            // Stale connection. Not active anymore
        }
    }
}
```

_______________________________________________________________________________
## Custom Authorizers
A custom authorizer is a Lambda function that is executed before processing a request. Custom authorizer returns an IAM policy that defines what Lambda functions can be called by a sender of a request.

Notice, that the result of a custom authorizer call is cached. A good practice is to provide access to all functions an owner of a token can.

```js
exports.handler = async (event) => {
  const token = event.authorizationToken
  // Check the token and return the IAM policy if accepted
  return {
    principalId: 'user-id', // Unique user id
    policyDocument: {
      Version: '2012-10-17',
      Statement: [
        {
          Action: 'execute-api:Invoke',
          Effect: 'Allow',
          Resource: '*'
        }
      ]
    }}};
```

_______________________________________________________________________________
# Databases
Selecting the Right Database for Your Application - AWS Online Tech Talks

https://www.youtube.com/watch?v=6K0Sds9Y2N0

## DynamoDB
DynamoDB is made of tables and is schemaless. The only thing that is enforced is a primary key. The database is organized as partitions based on a partition key.

AWS maintains 3 copies of the database in 3 different AZs in the region.

The primary key is made up of a partition key (hash key) and an optional sort key. The partition key is used to partition data across hosts for scalability and availability. The chosen partition key should have a wide range of values and is likely to have evenly distributed access patterns. For example CustomerId.

There is no limit on the number of items per partition key. For example, a customer could have multiple orders. The OrderId in this case can be used as a sort key.

### Scan
- Returns up to 1 MB of data
- If the data is larger than 1 MB, you need to use pagination to get all data.
- Scan returns `LastEvaluatedKey` if there is more data to return, which can be passed to the next Scan. It evaluates to Null if all data is read.

### Query
The Query operation finds items based on primary key values. The primary key can be a composite primary key (a partition key and a sort key).

### Composite key
A composite key in DynamoDB consists of two elements

- Partition key - what partition to write item to
- Sort key - to sort elements with the same partition key

Together - uniquely identify an item, meaning there can be no two items in a table with the same values of composite key.

NOTE. If a table has a composite key, there can be multiple items with the same partition key, providing they have different values of sort key.

Composite keys allows to perform queries, that can be used to get a subset of items with a specified partition key.

### Primary key
The primary key that uniquely identifies each item in an Amazon DynamoDB table can be simple (a partition key only) or composite (a partition key combined with a sort key).


### Index Types
DynamoDB supports two indexes types:

Local secondary index (LSI):

- Like an additional sort key
- Allows to sort items by a different attribute
- Added on the data in a table

Global secondary index (GSI)

- Allows to define a new partition key for the same data
- Allows to define a new partition and sort key for the same data
- Creates copy of the data in a new table (data is available via GSI after some delay) that can be queried using the new keys.

### Update Stream
The DynamoDB update stream is split into Shards, each of which gets updates from a certain partition.

### NoSQL Data Modelling
Creating a good data model upfront is very important and it cannot be changed later.
A good NoSQL data model depends more on the way the data is accessed rather than what the data looks like.

Define the access patterns:

- List all reading and writing patterns of the data.
- What aggregation patterns/queries we want to support.

Data modeling:

- Only 1 table for the service.
- Identify primaries keys.
- Define indexes for secondary access pattersn.

### Local DynamoDB instance
```sh
docker run -p 8000:8000 amazon/dynamodb-local
```

To interact with it:

```go
func NewDynamoDbStorage(region, tableName string, logger logrus.FieldLogger) (DB, error) {
    awsSession, err := session.NewSession(&aws.Config{
        Region:      aws.String("us-east-1"),
        Endpoint:    aws.String("http://127.0.0.1:8000"),
        Credentials: credentials.NewStaticCredentials("dummy", "dummy", "dummy"),
        LogLevel:    aws.LogLevel(aws.LogDebug),
    })
    if err != nil {
        return nil, err
    }
    ds := &dynamoDbStorage{
        dynamo:    dynamodb.New(awsSession),
        tableName: tableName,
        logger:    logger,
    }
    // Make sure the table exists
    ds.CreateTableIfNotExists()
    return ds, nil
}

func (ds *dynamoDbStorage) tableExists(name string) bool {
    tables, err := ds.dynamo.ListTables(&dynamodb.ListTablesInput{})
    if err != nil {
        ds.logger.WithError(err).Fatal("ListTables failed")
    }
    for _, n := range tables.TableNames {
        if *n == name {
            return true
        }
    }
    return false
}

func (ds *dynamoDbStorage) CreateTableIfNotExists() {
    if ds.tableExists(ds.tableName) {
        ds.logger.Printf("table=%v already exists\n", ds.tableName)
        return
    }
    _, err := ds.dynamo.CreateTable(buildCreateTableInput(ds.tableName))
    if err != nil {
        ds.logger.Fatal("CreateTable failed", err)
    }
}

func buildCreateTableInput(tableName string) *dynamodb.CreateTableInput {
    return &dynamodb.CreateTableInput{
        AttributeDefinitions: []*dynamodb.AttributeDefinition{
            {
                AttributeName: aws.String("modelID"),
                AttributeType: aws.String(dynamodb.ScalarAttributeTypeS),
            },
            {
                AttributeName: aws.String("version"),
                AttributeType: aws.String(dynamodb.ScalarAttributeTypeN),
            },
        },
        KeySchema: []*dynamodb.KeySchemaElement{
            {
                AttributeName: aws.String("modelID"),
                KeyType:       aws.String(dynamodb.KeyTypeHash),
            },
            {
                AttributeName: aws.String("version"),
                KeyType:       aws.String(dynamodb.KeyTypeRange),
            },
        },
        TableName:   aws.String(tableName),
        BillingMode: aws.String(dynamodb.BillingModePayPerRequest),
    }
}
```

_______________________________________________________________________________
# CloudFormation
A service that allows the creation and management of AWS resources.
See "Architecting on AWS" course materials for examples.

https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-template-resource-type-ref.html

```yaml
  Resources:
    # DynamoDB
    MyDynamoDBTable:
      Type: AWS::DynamoDB::Table
      Properties:
        # NOTE: DynamoDB is schemaless. Only put the items used in keys.
        AttributeDefinitions:
          - AttributeName: id
            AttributeType: S
        KeySchema:
          - AttributeName: id
            KeyType: HASH
        BillingMode: PROVISIONED
        TableName: ${self:provider.environment.GROUPS_TABLE}
        # (Optional) Global secondary index to allow querying by imageId
        GlobalSecondaryIndexes:
          - IndexName: ImageIdIndex
            KeySchema:
            - AttributeName: imageId
              KeyType: HASH
            Projection:
              # The new table includes projection of all fields in the original
              ProjectionType: ALL

    # RequestValidator
    RequestBodyValidator:
      Type: AWS::ApiGateway::RequestValidator
      Properties:
        Name: 'request-body-validator'
        RestApiId:
          Ref: ApiGatewayRestApi
        ValidateRequestBody: true
        ValidateRequestParameters: false
```

## Resource References
To reference a resource declared elsewhere in the template, we use the `Ref` keyword as `!Ref logicalName`. For example:

```yaml
MyStorageBucket:
    Type: AWS::S3::Bucket
BucketPolicy:
    Type: AWS::S3::Bucket
    Properties:
        PolicyDocument:
            - !Ref MyStorageBucket
```

## Multi-layer Infrastrucure
_Architecture tip:_
A best practice is to deploy infrastructure in layers. Common layers include the following:
- Networking
- Application
- Database

When using layers, you can re-use infrastructure templates between systems. For example, you can deploy a common network topology between Dev/Test/Production or deploy a standard database for multiple applications.

An AWS CloudFormation stack can also reference values from another stack. For example, the following is a portion of the lab-application template that references the lab-network template:

```yaml
Parameters:
  NetworkStackName:
    Description: >-
      Name of an active CloudFormation stack that contains the networking
      resources, such as the VPC and subnet that will be used in this stack.
    Type: String
    Default: lab-network

Resources:
  SubnetId:
    Fn::ImportValue:
    !Sub ${NetworkStackName}-SubnetID
```

_______________________________________________________________________________
# Kinesis
Kinesis is a data streaming service. Here is a good explanation about data streams in general:
https://www.youtube.com/watch?v=YqgnX0pYH2g

_______________________________________________________________________________
# Simple Notification Service (SNS)
SNS is a service to send messages to other services. _Publishers_ publish messages where _Subscribers_ consume incoming messages.

Publishers and subscribers communicate via topics:
- A publisher publishes a message to a topic.
- A subscriber receives a message if it is subscribed to a topic.
- One topic can have many subscribers.
- Subscribers can use various protocols: Lambda, HTTP, email, SMS, etc.

_SNS Topic Format_

`arn.aws.sns:<region>:<account-id>:<topic-name>`

_______________________________________________________________________________
# Key Management Service (KMS)
A service that stores our encryption keys and instead of using keys to encrypt data, we send the data to KMS and receive it back encrypted.

_______________________________________________________________________________
# AWS Secret Manager
- Designed specifically for storing secrets
- All values are encrypted.
- Pay-per-request
- Encryption done by KMS.

```js
const client = new AWS.SecretsManager()
const data = await client.getSecretValue(
  {SecretId: 'secret-id'}
).promise()
const secret = data.SecretString;
```

Caching the secret key:

```js
// Cache secret if a Lambda instance is reused
let cachedSecret: string

async function getSecret(sercretId, secretField) {
  if (cachedSecret) {return cachedSecret}
  const data = await client.getSecretValue(
    {SecretId: secretId}
  ).promise()
  cachedSecret = data.SecretString
  const secretObject = JSON.parse(cachedSecret)
  const secret = secretObject[secretField]
}
```

_______________________________________________________________________________
# Systems Manager Parameter Store (SSM)
- Designed for centralized confguration storage
- Values can be opitonally encrypted.
- Free.
- Encryption done by KMS.

_______________________________________________________________________________
# Labs

## IAM
Topics Covered:

By the end of this lab, you will be able to:

    Create an IAM policy using the visual editor.

Steps:

    Create a Policy
        On the AWS Management Console page, type IAM in the Find Services box and then select IAM.
        Click on Policies on the left-hand side.
        Click Create policy.
        Next to Service, click Choose a service.
        In the selection box, type S3.
        Select S3.
        Specify the actions allowed in S3 by clicking on List.
        Expand the Read action by clicking on the arrow next to it, then select GetObject.
        Next in the Resources section, ensure Specific is selected, and select the Any checkboxes next to bucket and object.
        Then click on Review policy.
        Enter a name for your policy in the Name box.
        Then click on Create policy.
    Review Policy
        After your policy is created, enter the name of the policy you just created in the Filter policies text box.
        Click on the name of your policy.
        Review the JSON for the policy you just created on the Permissions tab.
        Click on the Policy usage tab to see if this policy is in use. Notice this policy is not attached to any resources yet.


## Auto Scaling
Topics Covered:

By the end of this lab, you will be able to:

    Use auto scaling to launch EC2 instances
    Create an auto scaling group
    Test auto scaling

Steps:

    Create a Launch Configuration
        On the AWS Management Console page, type EC2 in the Find Services box and then select EC2.
        Scroll down to the Auto Scaling section on the left-hand menu and click Auto Scaling Groups.
        Click the Create Auto Scaling group button.
        Review the steps and click on Get started.

        Create a launch configuration by first selecting an Amazon Machine Image (AMI). In the row for Amazon Linux 2 AMI (HVM), SSD Volume Type, click the Select button.

        Note: An AMI is a template for an instance that indicates the operating system, an application server, and applications.

        Confirm that t2.micro is selected.
        Click Next: Configure details.
        Enter a name of your choosing in the Name field.
        Expand the Advanced Details section.
        Next to IP Address Type, click on Assign a public IP address to every instance.
        Click Next: Add Storage. Review the screen.
        Click Next: Configure Security Group.
        Ensure Create a new security group is selected.
        Click Review.
        Click on Create launch configuration.
        On the Select an existing key pair or create a new key pair, select Create a new key pair, enter a key pair name in the Key pair name field, and click Download Key Pair.
        Click on Create launch configuration.

    Create an Auto Scaling Group
        On the Create Auto Scaling Group page, enter a group name of your choosing in the Group name field, ensure the Group size is set to 1, for Network leave the default value. If no default value is shown, click on Create new VPC, and select the first Subnet by clicking in the Subnet field.
        Click Next: Configure scaling policies.
        Ensure that Keep this group at its initial size is selected.
        Click Review.
        Review the selected options and click Create Auto Scaling group.
        Click Close.

    Verify your Auto Scaling Group
        Verify that the group has launched your EC2 instance by first ensuring the auto scaling group you just created is selected and examining the Details tab shown on the bottom of the screen.
        Click the Activity History tab. The status of your instance should be Successful, which means the instance is launched.
        Click on the Instances tab. Notice the Lifecycle column states InService.

    Test Auto Scaling
        Click on the Instances tab.
        Under the Instance ID column, click on the blue Instance ID link.
        You will be taken to the Amazon EC2 console Instances page.
        Your instance should be selected.
        Click the Actions button, scroll down to Instance State, and select Terminate. Then select Yes, Terminate.
        In the left-hand navigation pane, click Auto Scaling Groups.
        Click the Instances tab. You will eventually see a new instance appear. If the new instance doesn’t appear, click refresh occasionally to update the list.
        Click on the Activity History tab to review the history for the Instance.

    Delete Auto Scaling Resources
        At the top of the screen, click the Actions button next to the Create Auto Scaling group.
        Click the Delete option.

## Cloud Watch

Topics Covered:

By the end of this lab, you will be able to:

    Create Cloud Watch event to react to the creation of an Amazon EC2 instance
    Send SNS notification via Cloud Watch when an event occurs

Steps:

    Create CloudWatch Rule
        On the AWS Management Console page, type cloud watch in the Find Services box and then select CloudWatch. The CloudWatch Dashboard appears.
        On the left-hand menu, under Events, select Rules.
        Click Create rule.
        For Service Name, select EC2.
        For the Event Type, select EC2 Instance State-change Notification.
        Select the Specific state(s) radio button. Select running from the drop-down box. Note: This configures the rule to trigger whenever an Amazon EC2 instance changes to the running state, which happens when an instance is launched or started.
        On the right-hand side of the screen, in the Target section, add a target by clicking on Add target.
        In the drop-down, change Lambda function to SNS topic.
        For the Topic, select the topic you created in the SNS hands-on exercise. Important: If the Topic doesn’t appear, the Access policy – optional section doesn’t have the correct permissions to allow other services to access the Topic.
        Scroll down and click the Configure details.
        Enter a name in the Name field. Ensure the state is Enabled. Click Create rule.
    Test CloudWatch Rule
        Navigate to the EC2 console page, by clicking on Services in the upper left-hand menu. Type EC2 in the text box and click on EC2 found in the search results.
        On the EC2 Dashboard page, click on Instances in the left-hand navigation.
        Click Launch Instance.
        Select the Amazon Linux 2 AMI (HVM), SSD Volume Type Amazon Machine Image (AMI). Important: You are free to choose a different AMI, but to avoid excessive charges, pick one that says, Free Tier Eligible.
        For the Instance Type, select the free-tier instance type of t2.micro.
        Click Review and Launch.
        Click Launch.
        Generate and download a new key pair and then launch the instance.
        Click Launch Instances.
        Click on View Instances.
        Once the Instance state changes to Running, check your email client for an email alert from the SNS Topic.
    Cleanup & Disable EC2 Instance and Cloud Watch Rule
        To avoid recurring charges for leaving an instance running, let’s disable the EC2 instance.
        From the EC2 Dashboard, select the instance just created, click Actions, then Instance State, and then select Terminate.
        To avoid recurring charges for leaving the Cloud Watch rule running, let’s disable it.
        From the SNS Dashboard, select Rules from under the Events section.
        Select the Rule you just created, by clicking the radio button next to the Rule.
        Click on the Actions button, and select Delete.


____
# AWS CLI

## Config
```sh
# Configure the default profile
aws configure
# Configure an additional profile
aws configure --profile=my-profile
```

The config is store in the following files

```sh
# ~/.aws/config
[default]
region = eu-north-1
output = json

# ~/.aws/credentials
[default]
aws_access_key_id=####
aws_secret_access_key=####
```

____
# Certification
- It's recommended to go through the FAQ for the needed components.

___
# Resources
- awsstash.com: A collection of AWS resources.
- CloudPing.info - Pings all AWS regions and returns their latency.
