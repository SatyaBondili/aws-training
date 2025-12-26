Table of Contents
- [1st AWS Service and total services as of now?](#aws-service-count)
- [AWS Global Infrastructure — 1st Region in US and 1st Region outside US?](#aws-global-infrastructure)
- [What happens when you add a file to Storage service like S3?](#s3-add-file)
- [AWS 6 pillars mnemonics?](#aws-6-pillars)
- [AWS Serverless Service means?](#aws-serverless)

<a id="aws-service-count"></a>
### [1st AWS Service and total services as of now?](#aws-service-count)

- SQS — Simple Queue Service. AWS provides over 175 services as of 2025.

<a id="aws-global-infrastructure"></a>
### [AWS Global Infrastructure — 1st Region in US and 1st Region outside US?](#aws-global-infrastructure)

- The first AWS region in the US is us-east-1 (Northern Virginia).
- The first AWS region outside the US is af-south-1 (Cape Town, South Africa).
- Every region contains multiple Availability Zones (AZs).

<img width="529" height="291" alt="AWS Regions" src="https://github.com/user-attachments/assets/25b46dae-cab0-4c6e-b089-91c9e3acb04b" />

<a id="s3-add-file"></a>
### [What happens when you add a file to Storage service like S3?](#s3-add-file)

When you upload a file (object) to Amazon S3, the object is stored redundantly across multiple Availability Zones within the selected region, providing high durability and availability. S3 assigns an object key and provides an addressable URL. You can configure metadata, permissions (ACLs or bucket policies), versioning, lifecycle rules, replication, and event notifications (for example, trigger a Lambda on object creation).

<img width="536" height="267" alt="AvailabilityZones-use" src="https://github.com/user-attachments/assets/19a71b6d-a89c-4db1-97d3-08261f5d5f8b" />

<img width="532" height="263" alt="web-applications-backup" src="https://github.com/user-attachments/assets/f5e8b1fd-c375-4a82-878d-362f60a19e42" />

<a id="aws-6-pillars"></a>
### [AWS 6 pillars mnemonics?](#aws-6-pillars)

PROCESS mnemonic for the AWS Well-Architected Framework pillars:
1. Performance
2. Reliability
3. Operational Excellence
4. Cost Optimization
5. Environmental (Sustainability)
6. Security

<a id="aws-serverless"></a>
### [AWS Serverless Service means?](#aws-serverless)

Serverless doesn't mean there are no servers; it means AWS manages the servers and infrastructure so developers only deploy code or configuration. Under the hood, AWS runs and manages the compute and runtime (for example, managed containers or platform runtimes) so you don’t have to provision or maintain the servers.
