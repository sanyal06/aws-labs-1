# AWS-SAA

## Day01

- Basics of Cloud Computing 
- [The NIST definition of cloud computing](https://nvlpubs.nist.gov/nistpubs/Legacy/SP/nistspecialpublication800-145.pdf)
- [Introduction and History of AWS](https://techcrunch.com/2016/07/02/andy-jassys-brief-history-of-the-genesis-of-aws/)
- [Certification Roadmap](https://aws.amazon.com/certification/)
- [AWS Global Infrastructure](https://aws.amazon.com/about-aws/global-infrastructure/)
- [Regions, Availability Zones, Local Zones](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-regions-availability-zones.html) and [Edge Network Locations](https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services/#AWS_Edge_Network_Locations)
- [Free tier account creation](https://aws.amazon.com/premiumsupport/knowledge-center/create-and-activate-aws-account/) and [coverage](https://aws.amazon.com/free/)
- Exploring the AWS Management Console
- [Setting up free tier billing alerts](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/tracking-free-tier-usage.html)
- [AWS Documentation](https://docs.aws.amazon.com/index.html)
- [Shared Responsibility Model](https://aws.amazon.com/compliance/shared-responsibility-model/) (to be revisited)

### [AWS Identity and Access Management](https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction.html)

<details>
  <summary>Owner's account AKA The root user</summary>
  
[The AWS Account Root User](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_root-user.html) and [only when to use it](https://docs.aws.amazon.com/general/latest/gr/aws_tasks-that-require-root.html)
</details>

<details>
  <summary>IAM Users</summary>
  
An AWS IAM user is an entity that you create in AWS to represent the person or service that uses it to interact with AWS. IAM Users have a set of permanent credentials such as an Access Key and/or Console ID-Password. You attach permission policies to the IAM user that determine what the user can and cannot do in AWS.
The console ID-password is used to access the services in the AWS account through the browser interface.
Access keys are a combination of an access key ID and a secret access key that are assigned to a user. These can be used to make programmatic calls to AWS when using the API in program code or at a command prompt when using the AWS CLI.
</details>

<details>
  <summary>IAM Groups</summary>
  
  If you find that you'll have several users who need similar permissions, you can define an IAM Group and associate your users to the group.
  
</details>

<details>
  <summary>IAM Policies (AWS Managed, Customer managed, Inline)</summary>
  
  By default, all permissions are denied unless explicitly granted. You may select predefined permissions from the list of AWS Managed Policies or define your own custom IAM policies.
  AWS Managed policies are common across all AWS customers. We can only use them but cannot modify/delete them. Customer-managed policies provide more precise control over your policies than AWS managed policies.
</details>

<details>
  <summary>IAM Roles (to be revisited)</summary>
  IAM Roles are used to provide temporary security credentials to any principal. One common case is allowing the EC2 service to distribute credentials to your application code running on an EC2 instance. Roles can also enable other scenarios in the enterprise such as cross-account access and identity federation.
  

</details>

<details>
  <summary>MFA</summary>
  
NA
</details>

### Network

- [VPC](https://aws.amazon.com/vpc/)
  - [Internet Gateway](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Internet_Gateway.html)
  - [Subnets](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Subnets.html#vpc-subnet-basics)
  - [RouteTables](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Route_Tables.html)
  - [NAT Gateway](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-nat-gateway.html), [NAT Instances](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_NAT_Instance.html); [Comparison](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-nat-comparison.html)
  - [Network ACLs](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-network-acls.html) (Stateless)
  - [Security Groups](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-security-groups.html) (Stateful) 
  - [Comparison of security groups and network ACLs](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Security.html)
  - [Elastic IP](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/elastic-ip-addresses-eip.html)

[Lab01](https://github.com/ashydv/aws-labs/blob/master/SAA-Lab01.md)

### Compute

- [EC2](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/concepts.html)
  - Creation Modification, Deletion
  - [Userdata, Metadata (Comparison)](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-instance-metadata.html)
  - [EC2 purchasing Options](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/instance-purchasing-options.html), [Tenancy](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/dedicated-instance.html)
  - Auto Scaling and Loadbalancing

## Day 02

- [VPC Peering](https://docs.aws.amazon.com/vpc/latest/peering/what-is-vpc-peering.html), [Transit Gateway](https://aws.amazon.com/transit-gateway/)
- [Site-to-Site VPN](https://docs.aws.amazon.com/vpn/latest/s2svpn/VPC_VPN.html)
- [Direct Connect](https://docs.aws.amazon.com/directconnect/latest/UserGuide/Welcome.html)
- [VPC Endpoints](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-endpoints.html) (to be revisited)

### Storage

- [Instance Stored Volumes](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/InstanceStorage.html)
- [EBS, EBS Volumes](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AmazonEBS.html)  
  - Types  
    - Creation, Modification, Snapshots, Deletion, Movement
- [S3](https://aws.amazon.com/s3/)
  - [Pricing](https://aws.amazon.com/s3/pricing/)
  - [Versioning](https://docs.aws.amazon.com/AmazonS3/latest/dev/Versioning.html)
  - [Static Website Hosting](https://docs.aws.amazon.com/AmazonS3/latest/dev/WebsiteHosting.html)
  - [Pre-signed url](https://docs.aws.amazon.com/AmazonS3/latest/dev/ShareObjectPreSignedURL.html)
  - [ACL](https://docs.aws.amazon.com/AmazonS3/latest/dev/S3_ACLs_UsingACLs.html) and [Bucket Policy](https://docs.aws.amazon.com/AmazonS3/latest/dev/using-iam-policies.html)
  - [S3 Storage Classes](https://aws.amazon.com/s3/storage-classes/)
  - [Replication](https://docs.aws.amazon.com/AmazonS3/latest/dev/replication.html), [Transfer Acceleration](https://docs.aws.amazon.com/AmazonS3/latest/dev/transfer-acceleration.html)
  - [Object lifecycle management]()https://docs.aws.amazon.com/AmazonS3/latest/dev/object-lifecycle-mgmt.html
- [Glacier](https://aws.amazon.com/glacier/)
- CLI and Roles Lab
- [CloudFront](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/Introduction.html)
- [Elastic File System](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AmazonEFS.html)
- [Storage Gateway](https://aws.amazon.com/storagegateway/), [good blog post](https://aws.amazon.com/blogs/storage/cloud-storage-in-minutes-with-aws-storage-gateway/) 
- [Snowball](https://docs.aws.amazon.com/snowball/latest/ug/whatissnowball.html) and [Snowmobile](https://aws.amazon.com/snowmobile/)

### Automation

- [CloudFormation](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/Welcome.html)
- [Elastic Beanstalk](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/Welcome.html)
- [OpsWorks](https://docs.aws.amazon.com/opsworks/latest/userguide/welcome.html)

### Application Integration/Decoupling

- SQS
- SNS
- SWF
- SES


[Lab02](https://github.com/ashydv/aws-labs/blob/master/SAA-Lab02.md)

## Day 03

### Databases

- RDS
  - Supported engines
    - Creation, modification and deletion
- ElastiCache
- DynamoDB
- RedShift

### Others

- Kinesis
- Route 53
- CloudWatch
- CloudTrail
- Trusted Advisor
- HSM
- ECS, ECR, EKS
- Lambda

[SAA-Lab03](https://github.com/ashydv/aws-labs/blob/master/SAA-Lab03.md)

### Wrap up

- [Simple Monthly Calculator](https://calculator.s3.amazonaws.com/index.html), [AWS Pricing Calculator](https://calculator.aws/#/), [AWS TCO Calculator](https://awstcocalculator.com/)
- [AWS Services quotas](https://docs.aws.amazon.com/general/latest/gr/aws_service_limits.html)
- Scope of service e.g. Global, Regional and AZ resources
- [Well-Architected Framework](https://d1.awsstatic.com/whitepapers/architecture/AWS_Well-Architected_Framework.pdf), [Online free training](https://www.aws.training/Details/Curriculum?id=42037)
- [AWS Events](https://aws.amazon.com/events/), reInvent, breakout sessions, aws.training, [whitepapers](https://aws.amazon.com/whitepapers/?whitepapers/), [customer case studies](https://aws.amazon.com/solutions/case-studies/), [this is my architecture](https://aws.amazon.com/this-is-my-architecture/)
- [AWS Blog](https://aws.amazon.com/blogs/aws/), [AWS Online Tech Talks](https://aws.amazon.com/events/online-tech-talks/)
