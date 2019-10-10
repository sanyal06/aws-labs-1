This script will show the EC2 instance ID on the webpage.  
```
#!/bin/bash
yum update -y
yum install httpd -y
systemctl start httpd
systemctl enable httpd
echo "Hello from EC2 instance ID: <b>$instanceid" > /var/www/html/index.html
```
