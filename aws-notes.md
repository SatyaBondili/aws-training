Table of Contents
- [1st AWS Service and total services as of now?](#aws-service-count)
- [AWS Global Infrastructure — 1st Region in US and 1st Region outside US?](#aws-global-infrastructure)
- [What happens when you add a file to Storage service like S3?](#s3-add-file)
- [AWS 6 pillars mnemonics?](#aws-6-pillars)
- [AWS Serverless service/architecture vs Server based architecture?](#aws-serverless)
- [AWS VPC (Virtual Private Cloud)](#aws-vpc)
- [How can i Architect cloud solution using amazon RDS](#aws-rds)


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
### [AWS Serverless service/architecture vs Server based architecture?](#aws-serverless)

* Serverless doesn't mean there are no servers; It means AWS provides and manages the servers, so developers need to deploy their code only.

#### Server based architecture where server running in personal Datacenter

<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/bc61de4d-532c-4bea-b884-1c464ee6a060" />

- As a IT team, if you want setup server, that hosts tomcat server which runs Java application, you need 2 things 1. Hardware and 2. Software.
- **Hardware:** You need computer with RAM, Operating System like windows or linux, Hard disk and CPU.
- **Software:** You need Tomat web server and Java Runtime to run both tomcat server and your java application.
- This server must run 24*7 eventhough business logic execution requires 10 mins time. Lets say java application which has business logic like batch job that runs every day once for 10 mins to syncs data from DB to salesforce. Moreover this server must be secured in your personal data center.

#### Server based architecture where server running in AWS Cloud EC2

<img width="1536" height="1024" alt="client-server-diagram-with-ec2" src="https://github.com/user-attachments/assets/14337d62-4477-4eab-949c-fad4ccee4baa" />

- **Hardware:** You need to setup EC2 instance with computing power like 0.1vCore. vCore includes CPU, RAM and Hard disk.
- **Software:** You need install Tomat web server and Java Runtime in EC2 instance to run your java application.
- **Drawback**: This EC2 instance also should be up and running 24*7 to run that 10 mins batch job.

#### Serverless architecture or Serverless services from AWS Cloud

<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/474b1cec-2f39-4915-a563-775fa025600a" />


- **Hardware:** Not Required.
- **Software:** Developer no need to setup application server but need to choose the server name from AWS available list and code technology. Lets say deploy code to AWS Lambda.
- **Advatange**: Lambda internally uses tomcat server to run that batch job code for that 10 mins. So you get billing cost for that 10 min run only. It is way bettern than using EC2 service.
- **Drawback**: AWS lambda max runtime is 15 mins.
<a id="aws-vpc"></a>
### [AWS VPC (Virtual Private Cloud)](#aws-vpc)
* Think AWS VPC as your personal data center in the AWS cloud.
* Why VPC exists: Isolation from other AWS customer's computers.
* Imagine AWS like massive city and VPC is your home.
* Network means a set of interconnected computers for sharing data over internet.
* VPC defination is: Logically isolated virtual network in AWS is called VPC.

#### How many VPC types are supported by Amazon?

2 types, Default VPC and Custom VPC.

**Default VPC:**
- When you create a new AWS account, Amazon automatically provides a Default VPC in every AWS Region.
- It has public subnet only and comes with a public subnet in every Availability Zone (AZ). Resources deployed in public subnet are accessable via internet. For example if you deploy Database in public subnet, then that database console is accessable via internet to perform CRUD operation. This is not suitable for Govt or Banking industry.
- It is for learning purpose only, don't use for enterprise applications development.
- Not ideal for production. Too open. Too lazy.
- Has:
  - Public subnets in each AZ.
  - Already Internet Gateway attached.
- Instances launched in it are automatically assigned a public IP address.
- Includes default security groups and network ACLs, no customization.

**Custom VPC:**
- A Custom VPC is one that you create manually from scratch. This is the standard for production environments where security and specific architecture are required
- Key benefits:
  - You define the CIDR block (IP range)
  - You decide how many subnets to create and whether they are Public or Private
  - You must manually create and attach the Internet Gateway or NAT Gateway
  - Routing tables
  - Public IP addresses are not assigned to instances automatically unless specified
  - Security rules
 
- Used for:
  - Production workloads
  - Enterprises
  - Anything serious
- This is what real architectures use.

**Simple flow example**

<img width="548" height="301" alt="image" src="https://github.com/user-attachments/assets/99c3dc78-4da2-4f2a-bef8-f295d2b691b9" />

<img width="424" height="245" alt="image" src="https://github.com/user-attachments/assets/9a2d4572-dff8-4c65-a64a-dcd6b0198a06" />

<a id="aws-rds"></a>
### [How can i Architect cloud solution using amazon RDS](#aws-rds)
* There are 2 ways to setup database AWS cloud.
  - 1. Install Oracle or other database in AWS EC2 instance.
  - 2. Use Amazon RDS service
* if you use EC2 instance, you need to install your database and also need to manage upgrades and patches.
* if you use RDS service, you no need to manage the database. RDS provides all type of databases with high scalability and availability

<img width="512" height="268" alt="image" src="https://github.com/user-attachments/assets/c6d66ee9-0621-4855-bdb2-ac25e35f568d" />
