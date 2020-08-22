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

## Storage Gateway
