# Amazon S3: Detailed Syllabus (SAA-C03 aligned)

## Module 1: Object Storage Fundamentals

- [ ] Block vs file vs object storage (EBS vs EFS vs S3)
- [ ] What S3 is and its use cases (backups, static sites, data lakes, logs, media)
- [ ] Buckets and objects: key, value, metadata, version ID, tags
- [ ] Flat namespace: "folders" are really key prefixes
- [ ] Bucket naming rules, global uniqueness, regional scope
- [ ] Object size limits (5 TB max, 5 GB single PUT)

## Module 2: S3 Architecture and Durability

- [ ] Data spread across multiple AZs
- [ ] 11 nines (99.999999999%) durability
- [ ] Availability by storage class
- [ ] Strong read-after-write consistency
- [ ] Request rates and prefix performance (3,500 PUT / 5,500 GET per prefix)

## Module 3: Working with S3

- [ ] Console: create bucket, upload, download, delete objects
- [ ] Multipart upload (when and why, parts, aborting)
- [ ] Transfer Acceleration
- [ ] Byte-range fetches
- [ ] Presigned URLs (upload and download, expiry)
- [ ] AWS CLI: `aws s3 cp`, `mv`, `rm`, `ls`, `sync`
- [ ] AWS CLI: `aws s3api` for low-level calls

## Module 4: Storage Classes and Cost Optimization

- [x] Standard
- [x] Intelligent-Tiering
- [x] Standard-IA
- [x] One Zone-IA
- [x] Glacier Instant Retrieval
- [x] Glacier Flexible Retrieval
- [x] Glacier Deep Archive
- [ ] Minimum storage duration and minimum object size charges
- [ ] Retrieval fees and retrieval tiers
- [ ] Pricing components: storage, requests, data transfer, retrieval
- [ ] Choosing the right class for a scenario

## Module 5: Lifecycle Management

- [ ] Transition rules (Standard → IA → Glacier)
- [ ] Expiration rules
- [ ] Cleaning up incomplete multipart uploads and old versions
- [ ] Filters by prefix, tag, and size
- [ ] Example: log retention policy

## Module 6: Versioning, MFA Delete, and Object Lock

- [ ] Enabling versioning and its states (unversioned, enabled, suspended)
- [ ] Delete markers and restoring older versions
- [ ] MFA Delete
- [ ] Object Lock: governance vs compliance mode
- [ ] Legal hold and retention periods
- [ ] Glacier Vault Lock

## Module 7: Security and Access Control

- [ ] Default private and Block Public Access settings
- [ ] IAM policies (identity-based)
- [ ] Bucket policies (resource-based)
- [ ] ACLs (legacy) and Object Ownership (BucketOwnerEnforced)
- [ ] How policies are evaluated together
- [ ] Cross-account access
- [ ] Bucket policy examples: public read, restrict by IP, enforce HTTPS, restrict to VPC endpoint
- [ ] VPC Gateway Endpoint for S3
- [ ] Access Points and Multi-Region Access Points

## Module 8: Encryption

- [ ] Encryption in transit (TLS)
- [ ] SSE-S3
- [ ] SSE-KMS
- [ ] SSE-C
- [ ] DSSE-KMS
- [ ] Client-side encryption
- [ ] KMS key policies, key rotation, request quota considerations
- [ ] Enforcing encryption through bucket policy
- [ ] Bucket Keys to reduce KMS cost

## Module 9: Replication and Data Protection

- [ ] Cross-Region Replication (CRR) vs Same-Region Replication (SRR)
- [ ] Prerequisites: versioning and IAM role
- [ ] What is and isn't replicated (existing objects, delete markers)
- [ ] Replication Time Control (RTC)
- [ ] Batch Replication for existing objects

## Module 10: Static Website Hosting

- [ ] Enabling website hosting, index and error documents
- [ ] Public access requirements and bucket policy
- [ ] Custom domain with Route 53 (bucket name must match domain)
- [ ] CloudFront in front of S3: Origin Access Control (OAC), HTTPS, caching
- [ ] CORS configuration and common errors

## Module 11: Event-Driven S3

- [ ] S3 Event Notifications to SQS, SNS, and Lambda
- [ ] EventBridge integration
- [ ] Use case: image upload triggers a Lambda that creates a thumbnail

## Module 12: Monitoring, Logging, and Analytics

- [ ] Server access logs vs CloudTrail data events
- [ ] CloudWatch metrics for S3
- [ ] S3 Inventory
- [ ] S3 Storage Lens
- [ ] Storage Class Analysis

## Module 13: Querying and Data Processing

- [ ] S3 Select and Glacier Select
- [ ] Querying S3 data with Athena (overview)
- [ ] S3 Batch Operations
- [ ] S3 Object Lambda (overview)

## Module 14: Hands-on Demos

- [ ] Demo 1: Create a bucket, upload files, explore the properties tabs
- [ ] Demo 2: CLI session: `sync` a local folder, `cp` with storage class, `ls --recursive`
- [ ] Demo 3: Enable versioning, overwrite and delete a file, then recover it
- [ ] Demo 4: Lifecycle rule moving objects to IA and Glacier
- [ ] Demo 5: Bucket policy and Block Public Access: private bucket vs public static site
- [ ] Demo 6: Presigned URL with expiry
- [ ] Demo 7: SSE-KMS encryption with a bucket policy that rejects unencrypted uploads
- [ ] Demo 8: Cross-region replication between two buckets
- [ ] Demo 9: S3 event triggering a Lambda
- [ ] Demo 10: Static website with CloudFront and OAC
- [ ] Optional: MinIO locally with Docker, using `aws --endpoint-url`

## Module 15: Common Exam Scenarios and Pitfalls

- [ ] Choosing between storage classes, encryption types, or replication options
- [ ] Accidental public exposure and how to prevent it
- [ ] "Cannot delete bucket" (versions, delete markers, multipart parts)
- [ ] Data transfer costs and same-region access
- [ ] Large file uploads: multipart plus Transfer Acceleration
- [ ] Recap quiz and cheat sheet

