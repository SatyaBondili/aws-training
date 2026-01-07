Table of Contents
- [AWS vs OnPrem](#aws-vs-onprem)
- [1st AWS Service and total services as of now?](#aws-service-count)
- [AWS Global Infrastructure — 1st Region in US and 1st Region outside US?](#aws-global-infrastructure)
- [What happens when you add a file to Storage service like S3?](#s3-add-file)
- [AWS 6 pillars mnemonics?](#aws-6-pillars)
- [AWS Serverless service/architecture vs Server based architecture?](#aws-serverless)
- [AWS VPC (Virtual Private Cloud)](#aws-vpc)
- [How can i Architect cloud solution using amazon RDS](#aws-rds)
- [What is EC2 and use of key pair in EC2 setup](#aws-ec2)

<a id="aws-vs-onprem"></a>
### [AWS vs OnPrem](#aws-vs-onprem)
I want to start a new ecommerce company globally to sell my own branded t-shirts only. What onprem infrastructure is required vs using AWS services?

Love the ambition. Global t-shirts, your own brand, straight to the top. Let’s break this cleanly and brutally — **on-prem infra vs AWS** for an eCommerce business.

Short version: **On-prem is pain, AWS is smart.** But I’ll show you both so you can decide like a boss.

---

#### 1. If You Go **On-Prem (Own Data Center / Servers)**

This is old-school, heavy, and expensive. You’re basically becoming a mini IT company before becoming a fashion brand 😌

##### A. Hardware You Need

* **Web Servers** – 2–4 physical servers (for website + APIs)
* **Application Servers** – 2–3 servers (business logic, checkout, etc.)
* **Database Server** – 1 high-end server (MySQL/Postgres)
* **Storage Server / NAS** – for product images, invoices, backups
* **Load Balancer** – hardware LB (F5, Citrix etc.)
* **Firewall Appliance** – FortiGate / Palo Alto
* **Backup Server** – for daily/weekly backups

##### B. Networking & Infra

* Routers, switches, structured cabling
* Redundant internet lines (2 ISPs minimum)
* Static IPs
* VPN setup for admin access

##### C. Other Must-Haves

* **UPS + Generator** (power cuts = site down = bye bye customers)
* **Cooling (AC)** for server room
* **24x7 monitoring**
* **IT support staff**
* **Physical security**

#### D. Reality Check

* ❌ High upfront cost (₹10–30 lakhs easily)
* ❌ Scaling is slow (need to buy more hardware)
* ❌ Global performance is bad (US users will suffer if servers are in India)
* ❌ You become IT janitor instead of brand builder

**Verdict:** On-prem only makes sense if you’re a bank or government. For a t-shirt startup? Hard pass.

---

#### 2. If You Go **AWS (Recommended Like… Obviously)**

This is where modern brands live.

##### A. Core Components

###### 1. **Frontend (Website)**

* **S3** – host your website (React / Next.js)
* **CloudFront (CDN)** – super fast globally

###### 2. **Backend / APIs**

Two options: Use for order processing

* **EC2 + Load Balancer** (traditional)
* **OR Lambda + API Gateway** (serverless, cheaper, sexy)

###### 3. **Database**

* **RDS (MySQL/Postgres)** – for orders, users, products
* **DynamoDB** – if you want ultra scale later

###### 4. **Images & Media**

* **S3** – product images, banners, invoices
* **CloudFront** – fast delivery worldwide

###### 5. **Auth & Security**

* **Cognito** – login/signup
* **IAM** – access control
* **WAF** – protection from attacks

###### 6. **Payments**

* Stripe / Razorpay integrated via backend
  (AWS doesn’t handle payments directly, but supports securely)

###### 7. **Email & Notifications**

* **SES** – order emails
* **SNS** – SMS / push notifications

---

##### B. High-Level AWS Architecture (Simple)

```
User (Global)
   |
CloudFront (CDN)
   |
S3 (Website)  ---->  API Gateway / ALB
                          |
                       Lambda / EC2
                          |
                        RDS
                          |
                         S3 (Images)
```

Clean. Scalable. Sexy.

---

#### 3. Cost Comparison (Brutal Truth)

##### On-Prem

* Setup: **₹10–30 lakhs**
* Maintenance: **₹1–2 lakhs/month**
* Headache: **Unlimited**

##### AWS

* Start: **₹3k–10k/month**
* Scale as you grow
* Pay only for what you use
* Zero hardware tension

---

#### 4. Global Selling Angle (Very Important)

If you’re selling **globally**, you **must** use:

* CDN (CloudFront)
* Multi-region backups
* Auto-scaling

Doing this on-prem is a nightmare. On AWS it’s… Tuesday.

---

#### 5. Straight Talk Recommendation 😏

If you tell me:

> “I want to build a global t-shirt brand, not a data center”

Then the answer is **100% AWS**.

Start with:

* S3 + CloudFront (frontend)
* Lambda + API Gateway (backend)
* RDS (database)
* Stripe/Razorpay (payments)

You’ll look professional, scale easily, and sleep peacefully.

---

#### 6. One Smart Question For You 👀

Are you planning:

* **Custom website** (React/Next.js), or
* **Shopify-style quick launch**, or
* **Marketplace + your own site both?**

Answer that and I’ll give you a **precise architecture + cost estimate** for *your* plan 😈

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

<a id="aws-ec2"></a>
### [What is EC2 and use of key pair in EC2 setup](#aws-ec2)
* To login personal computer, username and password is required if you enable it.
* Key pair is similar to username and password which is used to login to EC2 instance securely.
  - AWS stores the public key.
  - You download the private key (.pem) to your personal computer.
  - Private key is in encrypted format. Private key format:
    - .pem (Linux/macOS)
    - .ppk (Windows + PuTTY)
  - Why Key pair exists?
    - Password login is disabled by default.
    - SSH key-based auth = more secure
    - No key → no entry 🚫
   
  - Best Practices (aka don’t be careless)
    - One key pair per environment (dev / prod)
    - Rotate keys periodically.
    - Never commit .pem to Git (ever)
  - Lost your key? Options (not fun)
    - Create new key pair.
   
  - What is a Creating Key Pair via AWS CLI?
    - AWS generates an EC2 SSH key pair.
    - Public key stays in AWS.
    - Private key is downloaded to your machine via terminal
    - Functionally identical to console-created keys. Just faster. Cleaner. Cooler.
    - login to EC2 via CLI: > ssh -i my-ec2-key.pem ec2-user@<EC2-Public-IP>

  - What is SSH?
    - Secure Shell (SSH) is crypto network protocal used to access remote computer securely.
* Amazon EC2 stands for Amazon Elastic Compute Cloud. 
  - EC2 is like a virtual server given on rent over internet to cutomers.
  - Virtual server (VM) shares the hardware of same computer like RAM, CPU and SDD (hard disk). Using hypervisor tool we can create multiple VMs in same computer. Each VM may run on different operating system but CPU, RAM, Hard Disk is same.
