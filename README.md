# AWS_Certified_SA_Associate

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

# Athena and Macie

- Athena - SQL on S3. Pay per query and per TB scanned
- Quicksight. Visualise the reports
- Macie. Identifies personally identifiable information. Uses machine learning to recognise PII in s3 cloudtrail logs

# EBS

Cold
Magnetic - throughput optimised up to 500Mb/s
Instance store- lost following power cycle. OK for reboot (as storage is actually on hardware node)
Amazon Data Lifecycle Manager - Manage EBS snapshots

|---|---|---|---|---|
||Solid-state drives (SSD)||	Hard disk drives (HDD)||
|Volume type |	General Purpose SSD (gp2)|Provisioned IOPS SSD (io1)|	Throughput Optimized HDD (st1)	|Cold HDD (sc1)|
|Description|	General purpose SSD volume that balances price and performance for a wide variety of workloads|	Highest-performance SSD volume for mission-critical low-latency or high-throughput workloads|	Low-cost HDD volume designed for frequently accessed, throughput-intensive workloads|	Lowest cost HDD volume designed for less frequently accessed workloads|
|Use cases| Recommended for most workloads System boot volumes - Virtual desktops - Low-latency interactive apps - Development and test environments | -Critical business applications that require sustained IOPS performance, or more than 16,000 IOPS or 250 MiB/s of throughput per volume -Large database workloads, such as: -MongoDB -Cassandra -Microsoft SQL Server -MySQL -PostgreSQL -Oracle -Streaming workloads requiring consistent, fast throughput at a low price -Big data -Data warehouses -Log processing Cannot be a boot volume | Throughput-oriented storage for large volumes of data that is infrequently accessed Scenarios where the lowest storage cost is important Cannot be a boot volume ||
|API name|gp2|io1|st1|sc1|
|Volume size	|1 GiB - 16 TiB|	4 GiB - 16 TiB|	500 GiB - 16 TiB|	500 GiB - 16 TiB|
|Max IOPS per volume|	16,000 (16 KiB I/O) |	64,000 (16 KiB I/O) |	500 (1 MiB I/O)|	250 (1 MiB I/O)|
|Max throughput per volume|	250 MiB/s |	1,000 MiB/s |	500 MiB/s|	|250 MiB/s|
|Max IOPS per instance |	80,000|	80,000|	80,000|	80,000|
|Max throughput per instance |	2,375 MB/s|	2,375 MB/s|	2,375 MB/s|	2,375 MB/s|
|Dominant performance attribute|	IOPS|	IOPS|	MiB/s|	MiB/s|
