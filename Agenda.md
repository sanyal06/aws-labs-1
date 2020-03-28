# AWS-SAA

### Day01:

-   Basics of Cloud Computing
-   Introduction and History of AWS
-   Certification Roadmap
-   Global Infrastructure
-   Free tier account creation and coverage
-   Exploring the AWS Management Console
-   Setting up free tier billing alerts
-   [AWS Documentation](https://docs.aws.amazon.com/index.html)
-   [Shared Responsibility Model](https://aws.amazon.com/compliance/shared-responsibility-model/) (to be revisited)


**[IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction.html)**

<details>
  <summary>Users</summary>
  
An AWS IAM user is an entity that you create in AWS to represent the person or service that uses it to interact with AWS. You attach permission policies to the IAM user that determine what the user can and cannot do in AWS.
Access keys are a combination of an access key ID and a secret access key that are assigned to a user. These can be used to make programmatic calls to AWS when using the API in program code or at a command prompt when using the AWS CLI.
</details>

<details>
  <summary>Groups</summary>
  
NA
</details>

<details>
  <summary>Policies (AWS Managed, Customer managed, Inline)</summary>
  
AWS Managed policies are common across all AWS customers. We can only use them but cannot modify/delete them. Customer-managed policies provide more precise control over your policies than AWS managed policies.
</details>

<details>
  <summary>Roles (to be revisited)</summary>
  
NA
</details>

<details>
  <summary>MFA</summary>
  
NA
</details>

**Network**

-   VPC
    -   IGW
    -   Subnets
    -   RouteTables
    -   NAT Gateway, NAT Instance; Comparison
    -   NACL (Stateful)
    -   Security Groups (Stateless)
    -   NACL vs SG
    -   Elastic IP

**Compute**

-   EC2
    -   Creation Modification, Deletion
    -   [Userdata, Metadata (Comparison)](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-instance-metadata.html)
    -   EC2 purchasing Options, Tenancy

**Automation**

-   Elastic Beanstalk (to be revisited)
-   CloudFormation
-   OpsWorks


## Day 02:


-   VPC Peering, Transit Gateway
-   VPN Options
-   DirectConnect
-   VPC Endpoints (to be revisited)

**Storage**

-   EBS  
    -   Types  
    -   Creation, Modification, Snapshots, Deletion, Movement
-   S3
    -   Pricing
    -   Versioning
    -   Static Website Hosting
    -   Pre-signed url
    -   ACL and Bucket Policy
    -   S3 tiers
    -   CRR, Transfer Acceleration
    -   Life Cycle Policy
-   Glacier

-   CLI and Roles Lab

-   CloudFront
-   EFS
-   Storage Gateway
-   Snow family

**Databases**

-   RDS
    -   Supported engines
    -   Creation, modification and deletion
-   ElastiCache
-   DynamoDB
-   RedShift

Lab02

-   Autoscaling and Load balancing


## Day 03:


-   Kinesis
-   Route 53
-   CloudWatch
-   CloudTrail
-   Trusted Advisor
-   HSM

**Application Integration/Decoupling**

-   SQS
-   SNS
-   SWF
-   SES
-   ECS, ECR, EKS
-   Lambda

**Miscellaneous**

-   Simple Monthly Calculator, TCO Calculator
-   Limits
-   Scope of service e.g. Global, Regional and AZ resources
-   Well-Architected Framework
-   reInvent, breakout sessions, aws.training, whitepapers, customer use cases, this is my architecture
-   AWS Blog, AWS Online Tech Talks
