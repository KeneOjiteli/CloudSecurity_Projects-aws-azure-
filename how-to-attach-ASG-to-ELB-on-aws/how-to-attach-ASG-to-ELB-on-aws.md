# HOW TO ATTACH AUTO-SCALING GROUP TO ELASTIC LOAD BALANCER, AND HOW TO CONNECT AN EC2 INSTANCE USING EC2 INSTANCE CONNECT AND SSH CLIENT OPTIONS ON AWS

#### SERVICES REQUIRED
* #### IAM role with 2 permissions
* #### S3 to upload my source code to a bucket
* #### 1 EC2 instance, and an AMI of the instance
* #### Elastic Load Balancer
* #### Auto-Scaling Group

#### Steps
#### 1. Login to your AWS account
#### 2. Navigate to S3 and create a bucket (with a unique name)
![](images/asg.png)
#### 3. Upload source code to s3 bucket
![](images/asg1.png)
#### 4. Navigate to IAM dashboard and create a role with permission to have access to s3
![](images/asg2.png)
#### 5. Navigate to EC2 to launch an instance, give your instance a name
![](images/asg3.png)
#### 6. Choose a free tier eligible instance type, add key pair(which will be used to connect to your instance)
![](images/asg4.png)
#### 7. Add an already existing security group (which is a firewall for my ec2 instance)
![](images/asg5.png)
#### 8. Add user data, which is a script that runs only once at the start of my instance
![](images/asg6.png)
#### 9. I edited my user data because I had issues viewing my instance through the public IP because of some wrong syntax on the last line (this was a chalenge as it took me long to realize)
![](images/asg6_1.png) <br/><br/>
![](images/asg7.png) <br/><br/>
![](images/asg7_1.png)
#### 10. My site is visible after corrections
![](images/asg8.png)
#### 11. I created an AMI from my instance
![](images/asg11.png)<br/><br/>
![](images/asg12.png)
#### 12. Time to create a load balancer (an application load balancer in this scenario), with the necessary configurations
![](images/asg9.png)<br/><br/>
![](images/asg10.png)
#### 13. Next we create an auto-scaling group, note that all these services can all be found in the ec2 dashboard
![](images/asg13.png)
#### 14. When creating an ASG, it is necessary to create a launch configuration or a launch template (launch configuration in this case) where the following is added: AMI (which becomes a template for new instances to be created for the elastic load balancer), security group (new or existing SG), instance type and key pair
![](images/asg14.png)
#### 15. Add newly created launch configuration to ASG
![](images/asg15.png)
#### 16. Choose the default VPC and 2 availability zones
![](images/asg16.png)
#### 17. Attach ASG to already existing ELB (created in step 12), also add a target group
![](images/asg17.png)
#### 18. Specify desired capacity, minimum capacity and maximum capacity which ASG uses for automatic scaling based on demand.
![](images/asg18.png)<br/><br/>
![](images/asg19.png)
#### 19. Add email to get notified via an SNS topic whenever an instance is launched in my ASG
![](images/asg20.png)
#### 20. Add a name tag (this is optional)
![](images/asg21.png) <br/><br/>
![](images/asg22.png)
#### 21. Auto-scaling group is created
![](images/asg23.png)
#### 22. Using the DNS name of my ELb, my site is visible (best practice)
![](images/asg25.png)
#### 23. After establishing the fact that it is always best to access my site via the ELB and not from my instance or AMI, I edited the inbound rule for __http and https__ to allow traffic from the ELB (it was initially set to allow traffic from anywhere)
![](images/asg26_LI.jpg)
#### 24. Connecting to my instance via SSH client, this implies connecting to a machine remotely using the command line (this option was quite tricky, I attempted it severally as I had issues allowing the right inbound rule for SSH)
![](images/asg27.png)
#### 25. Note that to connect via SSH, I had to navigate to the folder that has my __key pair__ before connecting with my public DNS
![](images/asg27-1.png)
#### 26. I also connected using the EC2 instance connect option, which connects automatically to your ec2 instance on a browser
![](images/asg28-ic.png)
#### 27. In this method, a temporary SSH key is uploaded to the ec2 instance
![](images/asg28-ic-1.png)
#### 28. After this hands-on, I cleaned up by terminating my instance(s), deleting my ELB, detached my ASG (to avoid actively having some running instances)
![](images/asg29.png)

#### I learned the following:
* #### Each time my auto-scaling group is active, and I terminate any instance(s), based on the desired capacity I specified it always spins up 2 instances (such as in the diagram below) 
![](images/asg24.png)
* #### Each time an instance is stopped and restarted, the public IP changes
* #### An instance always takes time to become active more than one created from an AMI (a template) because most times, the instance built from scratch without an AMI has to download some packages compared to an AMI which is a template for a new instance
* #### For SSH, if you are not on the same network with AWS, it will be difficult setting inbound rule for SSH to my IP except a VPN is used, I set my inbound rule for SSH using custom as the source