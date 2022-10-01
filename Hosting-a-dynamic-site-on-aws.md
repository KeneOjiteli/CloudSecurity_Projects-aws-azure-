# HOSTING A DYNAMIC SITE ON AWS.

#### AWS SERVICES NEEDED: S3(for storage), EC2(to launch a virtual machine), & IAM(to assign role for S3 to interact with EC2)

#### Steps

##### 1. Login to your AWS account.
##### 2. Navigate to S3 to create bucket.
![](images/app.png)<br/><br/>
![](images/app1.png)<br/><br/>
![](images/app2.png)<br/><br/>
![](images/app3.png)<br/><br/>
##### 3. Upload source code from local machine as an object in just created S3 bucket.
![](images/app4.png)<br/><br/>
![](images/app5.png)<br/><br/>
![](images/app6.png)<br/><br/>
##### 4. Navigate to IAM dashboard to assign role to make EC2 access S3 / perform some actions.
![](images/app7.png)
##### 5. Under __Access management__ go to roles, click on __create roles__.
![](images/app8.png)
##### 6. Choose __AWS service__ as entity type, choose EC2 as use case.
![](images/app9.png)
##### 7. Search for S3 to grant permission, select __AmazonS3FullAccess__
![](images/app10.png)
##### 8. Give role a name, description and tag (this is optional), then click on create role button.
![](images/app11.png)<br/><br/>
![](images/app12.png)
##### 9. Notice that a new role has been created.
![](images/app13.png)
##### 10. Navigate to EC2, then instances to launch an instance.
![](images/app14.png)
##### 11. Give instance a name.
![](images/app15.png)
##### 12. Click __create new key pair__ to create key pair, which will be used to connect to my instance.
![](images/app17.png)
##### 13. Provide key pair name and ensure .pem is the private key file format; once key pair is created, ensure to save it as it will be needed to connect to instance.
![](images/app16.png)
##### 14. Create firewall/security to control traffic to instance.
![](images/app18.png)<br/><br/>
![](images/app19.png)
#### 15. Add role created using create new IAM profile on IAM instance profile; Click on launch instance to launch the instance with the configurations given.
![](images/app20.png)
##### 16. Instance has been launched.
![](images/app21.png)
##### 17. By default an instance state is __pending__ but changes to __running__ when it is ready to be used; View details of the selected instance
![](images/app22.png)
##### 18. To connect remotely(via ssh in this case), an external tool __MobaXterm__ will be used, open a session and choose SSH as session type. 
![](images/app23.png)
##### 19. Specify remote host, username, and path to private key, then click OK to get to the CLI.
![](images/app24.png)
##### 20. Run the commands below on the CLI, the function of each command is included by the side of each command.
![](images/app25.png)<br/><br/>
![](images/app26.png)
##### 21. Copy public IPV4 DNS from instance details and paste on a browser to view site; Notice that __apache__ test page is visible, this is because my html file is not named __index.html__ <br/><br/>
![](images/appa.png)
##### 22. To make my site visible, I renamed my html file to index.html, and re-enabled apache.
![](images/app27.png)
##### 23. I copied the public IPV4 DNS and my site is visible, notice the url.
![](images/app28_final.png)
##### 24. I terminated my EC2 instance, to avoid being charged.
![](images/app29.png)
