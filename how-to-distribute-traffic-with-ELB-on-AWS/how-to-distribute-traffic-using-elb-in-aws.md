# HOW TO DISTRIBUTE TRAFFIC BETWEEN TWO SERVERS USING ELASTIC LOAD BALANCER ON AWS

#### __Services required__
- #### EC2 - to create 2 EC2 instances
- #### Amazon AMI - to create a machine image, using this image to create another EC2 instance
- #### IAM roles - to create a role with permission to have full access to S3 and use aws session manager 
- #### S3 - to create bucket to store my code
- #### ELB - to evenly distribute traffic to 2 servers

#### __Steps__.
#### 1. Login to your AWS account, and navigate to IAM dashboard to create role
![](images/sm.png) <br/><br/>
![](images/sm1.png)
#### 2. Let entity type be AWS service, as we want 2 services to interact with each other.
![](images/sm2.png) <br/><br/>
![](images/sm3.png)
#### 3. Add 2 permissions, s3 full access and ssm managed instance core (to enable the use of aws session manger).
![](images/sm4.png)
#### 4. My role (newwebserverrole) has been created
![](images/sm5.png)
#### 5. Navigate to S3 and create a bucket, giving it a unique name
![](images/sm6.png)
#### 6. Bucket has been created.
![](images/sm7.png)
#### 7. Upload source code to newly created bucket
![](images/sm8.png)<br/><br/>
![](images/sm9.png)<br/><br/>
![](images/sm10.png)
#### 8. Navigate to EC2 to launch an instance with necessary configurations
![](images/sm11.png)<br/><br/>
![](images/sm12.png)<br/><br/>
![](images/sm13.png)<br/><br/>
![](images/sm14.png)<br/><br/>
![](images/sm15.png)
#### 9. Add the created role in IAM instance profile.
![](images/sm16.png)
#### 10. Add user data; user data performs common automated configuration tasks and runs scripts after the instance starts
![](images/sm17.png)
#### 11. Launch instance.
![](images/sm18.png)
#### 12. Instance is up and running (based on instance state and status checks), copy public IPV4 DNS and paste on browser to view site.
![](images/sm19.png)
#### 13. Site is visible.
![](images/sm20.png)<br/><br/>
![](images/sm21.png)
#### 14. Create an Amazon machine image (AMI) of the first EC2 instance.

#### An AMI makes it easy to launch another instance by copying the property/image/configuration of the EC2 instance, instead of starting from scratch to launch another instance
![](images/sm22.png)
#### 15. Creating an AMI from previously created instance
![](images/sm23.png)<br/><br/>
![](images/sm24.png)
#### 16. Instance from AMI is created
![](images/sm25.png)
#### 17. Status of AMI is pending (might take a while to change to available)
![](images/sm26.png)
#### 18. AMI is available and ready to use
![](images/sm27.png)
#### 19. Create a second server using AMI, To ensure high availability, I will host my site on 2 servers (in different AZs, just in case there is a failure in one AZ, which rarely happens)
![](images/sm28.png)<br/><br/>
![](images/sm29.png)
#### 20. I have launched 2 instances running on 2 different AZs (this is a best practice for high availability).
![](images/sm30.png)
#### 21. Site is visible on second EC2 instance (copy public IPV4 DNS and paste on browser)
![](images/sm31.png)
#### 22. Create a load balancer (load balancer can be found on EC2 dashboard); elastic load balancer is used to equally distribute traffic across instances (uses the concept of round robin)
![](images/sm32.png)<br/><br/>
![](images/sm33.png)
#### 23. Before creating ELB, security group has to be created
![](images/sm41.png)<br/><br/>
![](images/sm48.png)
#### Summary for ELB configuration
![](images/sm34.png)
#### 24. Creating Security group for ELB
![](images/sm35.png)<br/><br/>
![](images/sm36.png)
#### 25. In health check path, the '/' means it will test the home page (by default), to specify other pages include the path
![](images/sm37.png)
#### 26. Register target(s) to indicate server(s) that ELB will route traffic to (in this case, it will be routed to the 2 EC2 servers)
![](images/sm38.png)
#### 27. ELB has been created
![](images/sm39.png)
#### 28. ELB is currently active
![](images/sm40.png)

#### 29. Copy DNS name for ELB and paste on browser to view site, a best practice is to use ELB's DNS name to view site instead of public IPV4 DNS of EC2 because traffic goes to the ELB which evenly distributes to EC2 instance (the 2 servers are behind the ELB)
![](images/sm42.png)
#### 30. To show how load balancer works by indicating the exact server routed to at a particular time, Navigate to Systems Manager => Session manager, to start a session on my 2 servers, where I can use basic html and bootstrap to indicate the server traffic is routed to at each refresh
![](images/sm43.png)
#### 31. Navigate to __index.html__ and open a nano text editor
![](images/sm44.png)
#### 32. Editing code with html
![](images/sm45.png)
#### 33. Each refresh shows the server traffic is routed to (either web server 1 or web server 2)
![](images/sm46.png)<br/><br/>
![](images/sm47.png)
#### 34. I noticed that at step 23, using the ELB name was not working because I selcted 2 security groups, so I had to undo and select the right SG.
![](images/sm48.png)
