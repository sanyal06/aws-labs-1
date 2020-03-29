
# Deploying a Multi-Tier, Auto Scalable and Load Balanced Web Application using EC2 and RDS.

By the end of this lab exercise you would have deployed a PHP application that is highly available and on fault tolerant network infrastructure. This application uses Amazon RDS as a managed database to store the data.

The below picture is the representation of this lab exercise.

 ![](https://github.com/ashydv/aws-labs/blob/master/images/SAA-Lab02-Diagram.PNG)

The main services covered in this lab are –

- VPC
- RDS: MySQL
- EC2: Auto Scaling, Application Load Balancer
- SNS

PS: This lab is in continuation from VPC Lab 01, you should already have the VPC and other components from Lab 01 except NAT Gateway. This lab is also divided in two parts. We will create a single point of failure in the first part and remediate that in part two.

## Lab 02 – Part 01 of 02

Creating the database server and connecting to it from application server.

### Activity 01 – Creating an RDS instance

Navigate to the RDS service in management console.

Click on Create database.  
Choose a database creation method: Standard Create  
Engine options: MySQL  
Templates: Free tier

Settings -

- DB instance identifier: inventory-db
- Master username: master
- Master password: lab-password

DB instance size -  

- DB instance class: db.t2.micro  

Storage -  leave the defaults.

Availability & durability -  

- Multi-AZ deployment: Do not create a standby instance (Should be by default selected)

Connectivity -  

- Virtual Private Cloud (VPC): My_VPC
- Subnet group: my_dbsubnetgroup  
- Publicly accessible: No
- VPC security groups: Choose existing VPC security groups. Add DBSG from the dropdown and remove the preselected default.
- Availability zone: No preference

Additional Configuration -  

- Initial database name: inventory

Leave rest as default values and click Create database.

It will take a little time now to create your RDS instance, we can continue with the rest steps. Open another tab to do other steps and leave this page open, we will revisit soon.

Go to the EC2 dashboard and open the public dns endpoint of your My_WebServer in a browser window, the page would not load because of the port restrictions in the security group. Go Ahead and open the http port from anywhere in the My_LnxWebSG. You should now see the sample  web page with the instance details. Click on the settings button to set up database connection.

Go to the RDS dashboard and find out the database connection endpoint.

Return to the browser tab with the Inventory application and enter the below information:

- Endpoint: Paste the endpoint you copied earlier
- Database: inventory
- Username: master
- Password: lab-password

Click Save, the application will now connect to the database and will load some pre-fed sample data. Feel free to add, edit and delete inventory information using the web application.

So as of now you have one single EC2 instance serving a web application, it is storing the data in an RDS database. But this instance is a manually created and what will happen if it goes down? The data might remain saved in the database but will be unavailable till the time the server is/are brought back. The process has to be an automated one rather than manual, EC2 auto scaling is the feature that comes to rescue here!

Since we have installed our application and did the configurtion already, let us save this as an image for our future use so we dont have to start from scrach.

On the EC2 dashboard, select the instance, go to the Action dropdown, Image and create image. Note the AMI ID, we will use it later.

Terminate the instance, we are simulating a disaster now!

## Lab 02 – Part 02 of 02

You will now be launching this application using a Launch Configuration into an Auto Scaling Group, the ASG will automatically grow and shrink the number of your servers based on the user defined threshold. The requests to your application will be distributed by Application Load Balancer.

### Activity 04 - Creating an Auto Scaling Group

Go to the Auto Scaling section in your EC2 dashboard and click on Create Launch Configuration.

- AMI: Select the AMI from MyAMI section that you created in previous steps.
- Instance Type: t2.micro
- Name: MyAppServer_V01_LC
- IAM Role: My_SSMRole

Go next.

- No additional storage, go next.
- On the security group page, choose My_LnxWebSG
- Click on Create launch configuration
- Create a new key pair or select the existing and Create launch configuration

Your Launch Configuration is created, let us now create the auto scaling group. Click on Create an Auto scaling group using this Launch configuration.

- Group name: MyApp_ASG
- Group size: Start with 2 instances
- Network: My_VPC
- Subnet: Select both the public subnets here.
- Configure scaling policies: Use scaling policies to adjust the capacity of this group
- Scale between 2 and 6 instances.
- Target value: 60
- Instances need: 10
- Next Configure Notification
- Add Notification: Create Topic
- Send a notification to: MyASG_Topic
- With these recipients: 'your email ID'
- Next Create a Tag with 'Key: Name' and 'Value: MyAppServer'
- Review: Create Auto Scaling group

Click on Close, you would be directed to the Auto Scaling Groups Dashboard. Explore the Activity History and other tabs.

You have just launched our highly available inventory application in an ASG. You can open the public IP addresses of both the instances in separate browser and see what happens. You should be seeing the webpage with same information but look at the bottom. You should see the instance ID. This way you can identify which server your request is being served from.

Also check if you received an email from SNS topic, you need to confirm the subscription.

But the end users would not have IP addresses to your server right? They should have a domain name to go to. Let us create a Load balancer that will divert the traffic to both these instances in round robin method.

### Activity 05 - Creating an Application Load Balancer

Go to the Load Balancing section of EC2 dashboard and click on Target Group

- Create Target Group
- Target group name: MyTG
- VPC: My_VPC
- Leave rest defaults and click Create.

Click on Load Balancers: Create Load Balancers

From next screen, create an Application Load Balancer

- Name: MyALB
- Scroll down to the Availability Zones Section
- Select the VPC in which you have launched the ASG
- Select Public Subnets from both AZs. This is a critical step, reconfirm before going forward.
- Next - Configure Security Settings – Ignore the warning, it is recommending to have SSL certificate.
- Next - Configure Security Groups. Select My_ELBSG from existing ones.
- Next Configure Routing –
- Target group – Existing Target Group
- Name: MyTG
- Leave rest defaults - Register Targets – Review – Create

Click on close and it will take you to the load balancer dashboard, you should see the DNS endpoint of your load balancer in Description Tab. ALB takes a little time to come up. Refresh till you see the state as active.

Let us register our instances in ASG with the MyTG target group. Select your ASG and go to action dropdown and click on edit. You will find a field for target group in the lower section. Click on the empty field and assign MyTG. Save it (save button is towards the top right of lower section)


Open the DNS address of your ALB in a browser and notice what it shows. It is now diverting the traffic to both your instances. You can see the behavior of load balancer while you refresh the page and notice the instance ID.

So at this point of time your application can be reached by the load balancer endpoint as well as direct IPs of the instances. This is not an ideal behavior, we should not allow our app servers to accept traffic from anywhere else apart from the load balancer in order to ensure security.

Can you restrict it?

### Activity 06 – Modify the Security Groups to ensure security on incoming traffic

Update the **My_LnxWebSG** security group settings as shown below.

#### My_LnxWebSG

| Type  | Protocol | Port Range | Source |            |
| :---: | :------: | :--------: | :----: | :--------: |
| HTTP  |   TCP    |     80     | Custom |  My_ELBSG  |
| HTTPS |   TCP    |    443     | Custom |  My_ELBSG  |
|  SSH  |   TCP    |     22     | Custom | My_WinBHSG |
|  SSH  |   TCP    |     22     | Custom |  LnxBHSG>  |

If your application is reachable only through the load balancer endpoint and not through visiting the IP addresses or EC2 instances in browser, you have done it well.

You can also now try deleting one/more server in order to verify whether the auto scaling feature is able to spin up instances in response.

### Clean up steps –

Delete the resources in the below order

 1: RDS (do not create a snapshot and do not retain the automated backup files)  
 2: ALB  
 3: Auto Scaling Group (takes little time to delete)  
 4: Target Group – Launch Configuration.

***All the services used in this lab are eligible and covered within the free tier account. There should not be any charge if you delete all the resources within a couple of hours of creation provided you have monthly limits left.***

### Lab Complete!
