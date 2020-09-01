# AWS_Certified_SA_Associate

Notes are based on the fact that the Devops and SysOps exams have been passed, just the differences added.

## AWS Support Plans

- *Basic*  - Free. Access to Customer service
- *Developer* - $29/month. 1 Account holder
- *Business* - $100/month. Guaranteed response time, support API
- *Enterprise* - $15000/month. SA, Technical Account Manager, Support Concierge

## S3
0 - 5TB object storage.

### URLs for static hosting
https://bobbins.s3amazonaws.com
https://bobbins.eu-west-1.amazonaws.com

### S3 Storage types
|Type|Availability|Durability|Cost|
|---|---|---|---|
|S3 Standard | 99.99   | 99.999999999 (11*9s)  | $$$   | 
|S3 IA   | 99.9   | 11*9s  | $$  | 
|S3 1 Zone IA   | 99.5   | 11*9s  | $   | 
|S3 Intelligent Tiering |99.9 | 11*9s | Depends on the chosen tiering |

- Glacier Select can be used to retrieve a subset of an archive
- Amazon S3 Select. csv/json support gzip / bzip Enables applications to retrieve only a subset of data from an object by using simple SQL expressions.
- Object Lock - WORM. S3 or Glacier objects or buckets/archives. Can be for a fixed time or permanent.
- Governance Mode. Special perms required to overwrite or delete. Can grant perms to alter retention or delete if necessary.
- Compliance Mode. No changes allowed.
- Retention Period. Expires or can be overwritten after this time.
- Legal Hold. No retention period. Locked until s3:PutObjectLegalHold run.
- Glacier Vault Lock

## AWS Organisations and Consolidated Billing

- Service Control Policies disable paying account from creating EC2 services etc.
- Allow shared resources/Reserved EC2 instances.

## AWS Datasync (On Prem->AWS)

AWS DataSync makes it simple and fast to move large amounts of data online between on-premises storage and Amazon S3, Amazon Elastic File System (Amazon EFS), or Amazon FSx for Windows File Server

- Move large amounts of data from On-prem to AWS
- NFS + SMB
- Replication is carried hour Hourly, Daily, Weekly
- Install Datasync Agent
- EFS - EFS

## CloudFront

When you want to use CloudFront to distribute your content, you create a distribution and choose the configuration settings you want. For example:

- Your content origin—that is, the Amazon S3 bucket, MediaPackage channel, or HTTP server from which CloudFront gets the files to distribute. You can specify any combination of up to 25 Amazon S3 buckets, channels, and/or HTTP servers as your origins.
- Access—whether you want the files to be available to everyone or restrict access to some users.
- Security—whether you want CloudFront to require users to use HTTPS to access your content.
- Cache key—which values, if any, you want to include in the cache key. The cache key uniquely identifies each file in the cache for a given distribution.
- Origin request settings—whether you want CloudFront to include HTTP headers, cookies, or query strings in requests that it sends to your origin.
- Geo-restrictions—whether you want CloudFront to prevent users in selected countries from accessing your content.
- Access logs—whether you want CloudFront to create access logs that show viewer activity.

Signed URL :
Require that users access your private content by using special CloudFront signed URLs or signed cookies.
Require that your users access your content by using CloudFront URLs, not URLs that access content directly on the origin server (for example, Amazon S3 or a private HTTP server). Requiring CloudFront URLs isn't necessary, but we recommend it to prevent users from bypassing the restrictions that you specify in signed URLs or signed cookies.

## Storage Gateway

Appliance used to connect on-premise with cloud storage.

- File Gateway  - NFS + SMB -> S3
- Volume Gateway - ISCSI block storage locally and also performs EBS Snapshots
- Stored Volumes -> Entire Datacentre -> AWS S3 Backing
- Cached Volumes -> Local Cache-> AWS S3 Backing
- Tape Gateway. Virtual Tape Library (VTL)- iscsi devices

## Athena and Macie

- Athena - SQL on S3. Pay per query and per TB scanned
- Quicksight. Visualise the reports
- Macie. Identifies personally identifiable information. Uses machine learning to recognise PII in s3 cloudtrail logs

## EBS

- Magnetic - throughput optimised up to 500Mb/s
- Instance store- lost following power cycle. OK for reboot (as storage is actually on hardware node)
- Amazon Data Lifecycle Manager - Manage EBS snapshots

||Solid-state drives (SSD)||	Hard disk drives (HDD)||
|---|---|---|---|---|
|Volume type |	General Purpose SSD (gp2)|Provisioned IOPS SSD (io1)|	Throughput Optimized HDD (st1)	|Cold HDD (sc1)|
|Description|	General purpose SSD volume that balances price and performance for a wide variety of workloads|	Highest-performance SSD volume for mission-critical low-latency or high-throughput workloads|	Low-cost HDD volume designed for frequently accessed, throughput-intensive workloads|	Lowest cost HDD volume designed for less frequently accessed workloads|
|Use cases| Recommended for most workloads System boot volumes - Virtual desktops - Low-latency interactive apps - Development and test environments | -Critical business applications that require sustained IOPS performance, or more than 16,000 IOPS or 250 MiB/s of throughput per volume -Large database workloads, such as: -MongoDB -Cassandra -Microsoft SQL Server -MySQL -PostgreSQL -Oracle -Streaming workloads requiring consistent, fast throughput at a low price -Big data -Data warehouses -Log processing Cannot be a boot volume | Throughput-oriented storage for large volumes of data that is infrequently accessed | Scenarios where the lowest storage cost is important Cannot be a boot volume |
|API name|gp2|io1|st1|sc1|
|Volume size	|1 GiB - 16 TiB|	4 GiB - 16 TiB|	500 GiB - 16 TiB|	500 GiB - 16 TiB|
|Max IOPS per volume|	16,000 (16 KiB I/O) |	64,000 (16 KiB I/O) |	500 (1 MiB I/O)|	250 (1 MiB I/O)|
|Max throughput per volume|	250 MiB/s |	1,000 MiB/s |	500 MiB/s|	250 MiB/s|
|Max IOPS per instance |	80,000|	80,000|	80,000|	80,000|
|Max throughput per instance |	2,375 MB/s|	2,375 MB/s|	2,375 MB/s|	2,375 MB/s|
|Dominant performance attribute|	IOPS|	IOPS|	MiB/s|	MiB/s|

## ENI vs ENA vs EFA

- *ENI* Elastic Network Interface is a NIC. Multiple ENI can be added.
- *EN* Enhanced Networking. High performances networking on support instance types. SRV-IOV - High network throughput, low CPU overhead, high PPS, Low latency. 10->100Gb/s. Instance types, ENA better than VF
- *EFA* Elastic Fabric Adapter is a network interface for Amazon EC2 instances that enables running applications requiring high levels of inter-node communications at scale on AWS. EFA are attached to an EC2 instance to accelerate high performance computing and machine learning applications.
- *ENI* attach.  You can attach a network interface to an instance when it's running (hot attach), when it's stopped (warm attach), or when the instance is being launched (cold attach). 

## Spot Instances

- Bid on EC2 instance time based on market rates
- Spot block - prevent spot instances from being switched off for 1-6 hours
- Spot Fleet. A collection, or fleet, of Spot Instances, and optionally On-Demand Instances. Launch the number of spot instances and optionally on-demand instances to meet the target capacity. The request is fulfilled if there is capacity and cost matched.
- Spot instance pools. Using multiple pools, can choose the size, the instance type and price.

## EC2 Hibernate.

- Similar to suspend for laptops. Memory is written to EBS and then suspended. When it is unsuspended, the memory is re-populated. Only works for <150GB RAM instances. Useful for pre-warming autoscaling groups.

## EC Placement Groups

- Cluster. Kept together for high IOPs  [ x x x x ]
- Distributed/Spread. Separate racks/ AZ for HA. [ x ] [ x ] [ x ]
- Partitioned (Spread Cluster). Clustered together, but clusters of servers spread over AZs/Racks [ x x x x ] [ x x x x ]

## Amazon FSx for Windows Fileservers

Amazon FSx for Windows File Server provides fully managed Microsoft Windows file servers, backed by a fully native Windows file system. Amazon FSx for Windows File Server has the features, performance, and compatibility to easily lift and shift enterprise applications to the AWS Cloud.

- SMB (Not SAMBA)
- AD users
- ACLs
- DFS

## Amazon FSx For Lustre. 

Used for Massive datasets and huge IOPS compared to EFS. Not Windows. You use Lustre for workloads where speed matters, such as machine learning, high performance computing (HPC), video processing, and financial modeling.

## HPC 

AWS Batch. Multi Node Parallel jobs and scheduled jobs. AWS Parallel cluster

## RDS

Cross Region Read replicas now available.

## DynamoDB
 
- NoSQL database built on SSDs and 3 AZs in one region
- Eventually consistent Reads
- Strongly consistent reads.
- 4K Reads (2 eventually consistent, 1 strongly consistent)
- 1K Writes
- Units rounded to the nearest 4K/1K.
- Also available in pay per request pricing, but pay more than provisioned pricing.
- On demand backup and restore. Full backups anytime, 0 impact on performance. 
- Consistent within seconds, retained until deleted. Operates in the same region as source table.
- Point in time recovery. 30 day retention.


### DAX for DynanoDB 

- HA, in memory cache
- 10 x Performance improvement
- Through cache to Dynamo DB

### Dynamo DB Streams

- Time ordered sequence of item level changes in a table retained for 24 hours inserts, updates and deletes. Can be used to trigger lambda functions.

### Global Table

- Replicate global table from one region to another using streams.
- Multi master, multi-region.

## Database migration service

- Any <-> Any database migration. Dynamo DB is not supported source database.

## AWS Directory Service

- AWS Resources with on Prem ADS
- AWS Management console with on premise AWS.
- Group policies based on LDAP, DNS, Kerberos, NTLM authentication.
- AWS Managed Microsoft AD - Windows Domain controllers in AWS.
- AWS Manage some of the service - [ AZ Split, Patching, Rotation], Customer manages some of the service - [ Users, Groups, Scaling out DC Trusts, CA Federation ] 

## Simple AD - Standard managed directory.

- Based on Samba, suitable for <500 users. Cannot join existing on-premise AD as it does not support trust.

## AD Connector

- Direct Gateway proxy for on-prem AD avoids caching.

## Cloud Directory

- Directory store for development

## Amazon Cognito User Pools

- Managed user directory for SaaS applications, can authenticate against Facebook, Google etc.

## IAM Policies

- ARN. Unique ID for AWS Resolution. arm:partition:service:region:accountid_resource APSRAR.
- Is a json document. Identity policy - attach to person. Resource Policy. Attach to a resource. 
- Has no effect until it is attached.
- Effect. Action. Resource. E.A.R
- Deny > Allow
- AWS Managed Policies (pre rolled) versus Customer Management policies (roll your own)
- Inline policy, don't use unless temporary.
- AWS Joins all applicable policies.
- Permission boundaries, delegate admin to other users, prefvent privilege escalations, control maximum permissions on a object. This is used so that it's possible to have full administrator access from policy, but it only apply to S3 (permission boundary).

## Resource Access Manager

- Resource sharing with other Accounts.
- App Mesh, Aurora, Code Build, EC2, EC2 image builder
- Can launch EC2 instances in a shared subnet

## AWS Single Sign-On

- Dropbox, Github.
- Sign into AWS using AWS Single Sign on 
- AD Trust 
- SAML can authorize against it (so can use this to auth 3rd party apps using AWS)
- SAML is associated with Single sign on.

## VPC

- Associate a security Group with a subnet
- Network ACL -> You can associate a network ACL with multiple subnets. However, a subnet can be associated with only one network ACL at a time. When you associate a network ACL with a subnet, the previous association is removed. Rules are numbered within the ACL low to high.

## Global Accelerator
- Speed up requests using Amazon backbone and smart routing. Cloudfront is HTTP/HTTPS only, Global Accelerator applies to TCP/UDP.

## Gateway endpoint

- Access AWS Resources without traversing IGW

## AWS Private Link

- Open service to another VPC without VPC Peering. Can Apply to many VPCs. Traffic from VPC0 can traverse VPC1, transit to another VPC2 (separate customer) using Private link, but no link required between VPC0 and VPC2.

## AWS Transit Gateway

- Hub for many VPC, is a hub and spoke service which can be used to simplify networ architecture.

## VPN CloudHub

Hub/spoke to allow VPNS in remote office to talk to each other

## AWS Network costs

Traffic is free within AZs, Cost between AZs, Cost between regions.


## Load Balancers

- Classic load balancers. HTTP/HTTPS only
- Application load balancers. Path/Host detection, routing
- Network Load balancers. High performance layer 4.
- Application load balancers have lifecycle hooks which can wait before startup/termination.
- X-Forwarded-For, Sticky sessions.
- Cross-Zone load balancers, pass ELB traffic to zones

## Autoscaling

- Config templates [ AMI, Type, Key pair, Security Group]
- Scaling options [ Maintain, scale manually, schedule, scale on demand, predictive scaling ]

### Autoscaling Groups

- Lifecycle Hooks puts instance into wait state before termination. Default 1 hour.

### Scheduled Scaling

- Scheduled action. Start time, new min, new max, new desired. One Shot / Recurring
- Predictable load Pattern

### Launch configuration (older)

- Named document contains AMI, Instance type, ssh keypair, security group, instance profile, block device mapping, user data.

### Launch template (new and better)

- Named document contains AMI, Instance type, ssh keypair, security group, instance profile, block device mapping, user data. Can also use it for spinning up one-off EC2 instances or launching a spot fleet. It is more flexible. It is versioned.

### Autoscaling options

- ChangeInCapacity - add 2 when load increases
- ExactCapacity - scale to 6
- PercentageChangeInCapacity - Add 50%
- Cooldown period. After scaling wait this long before taking further actions (covers spin up time)

### Step scaling
If demand rapidly increases

- Lower Bound
- Upper Bound
- Adjustment Type
- Amount to increase desired capacity
- Warm up time.

### Target Tracking

Metric and Target value. Cloud Watch Alarm Created and scaling policy. CPU is good example. Scale out and Scale in Warm up time.

## Elastic Beanstalk

- Compute service, full provisioning. Provisions on EC2 and autoscaling groups. Deploy containers.

## On Premise

- DMS- Database migration service
- SMS - Server migration service
- AWS Service Application Discovery service. Service map is build from ta running VM.
- VM Import/Export.

## SQS 

- Used for decoupling applications.
- 256KB Text
- 2GB -> S3 can be retrieved from S3.
- Standard and FIFO queues.
- Visibility Timeout is the time the message is invisible in the queue after a read. This can lead to double messages if the reader drops the message. 12 hours is the maximum.
- Long polling, holds onto a read request in the case of an empty queue to prevent the CPU of the polling process from being maxed out.
- 14 day retention.
- Delay
- DelaySeconds. How long after a message is added to the queue before it can be  consumed.

## SWF 

- Actors
- Workflow starters, initiate a workflow.
- Decider- Control the flow of activity
- Activity worker. Do the work.


## SNS

- Pub/Sub messages to a topic.
- No polling. Push mechanism
- PAYG

## API Gateway

- Think of this as a front door to lambda, dynamo db, EC2.
- Define an API, Define resource (URL path), HTTP Methods, End points
- API Caching. TTL for Common requests.
- CORS - Cross object resource sharing. Origin policy cannot be read on remote resources.

## Kinesis

### Kinesis Streams

Producers->Stream->Kinesis Streams->Sharding->EC2 Consumers, DynamoDB, Redshift, S3, RDS
Per shard performance. 5 transactions/second, 2MB/s, 1000 Record/second writes, 1MB/s writes. Increase the data capacity by increasing the shards.

### Kinesis Firehose

Producers-> Firehose lambda functions No persistence-> Redshift/S3/Elasticsearch

### Analytics

Analyse data on fly from either Streams or Firehose.

## Web Identify Federation and Cognito

Mobile Application services map to IAM role. Cognito Push Sync

### User Pool - Authentication
Sign up and Sign in for users. JSON web token (JWT)

### Identify Pool - Authorization
Temporary authorization to AWS Services.

## Event Driven Applications

Event Driven Architecture. PUB/SUB->SNS Topic Broadcast
DLQ - Dead letter queue
SNS uses dead letter queue
SQS- > MaxReceiveCount
Lamdba - Failed Asynchronous Invocation
S3 Event Notification API -> SQS, SNS, lamdba.

### Fanout
PUB = SNS
SUB = SQS1, SQS2, etc.

S3 Events - PUT, REMOVE, Restored from Glacier, RRS Object Lost, Replication issues.

## KMS 
Regional key managent service.

- Customer Master Key
- S3 Objects, DB Password, API keys
- Encrypt up to 4KB
- Pay per Call
- CloudTrail logs encryption

## KMS

|Type of CMK|	Can view CMK metadata|	Can manage CMK	|Used only for my AWS account|	Automatic rotation|
|---|---|---|---|---|
|Customer managed CMK|	Yes|	Yes|	Yes|	Optional.| Every 365 days (1 year).|
|AWS managed CMK|	Yes|	No|	Yes|	Required.| Every 1095 days (3 years).|
|AWS owned CMK|	No|	No|	No|	Varies|
|---|---|---|---|---|

## SAM

- Serverless Application Model
- CloudFormation Extension for Serverless functions, APIS, tABLES. 
- Supports all CloudFormation
- Run Serverless Applications Locally
- Packages Deploy using Code Deploy

## ECS

Elastic Container Store (ECS. Manage clusters of EC2 Servers for containers. 
Fargate - No EC2.
Elastic Container Services - Can use Fargate for Servless containers.

- *Cluster* logical collection of instances
- *Task Definition* - similar to a dockerfiles
- *Container Definition* - Controls CPU and Memory + Port Mapping
- *Task* - Single running copy of container
- *Service* - Provides Scaling Min/Max

## EKS

Elastic Kubernetes Services -Can use Fargate for Serverless Kubernetes

## Redshift

- Data warehousing.
- Enhanced VPC Routing provides provides VPC resources access to redshift.


