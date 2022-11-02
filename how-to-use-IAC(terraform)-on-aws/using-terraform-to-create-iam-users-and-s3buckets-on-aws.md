# LEARNING THE BASICS OF TERRAFORM BY CREATING S3 BUCKET AND IAM USERS

#### Terraform is an infrastructure as code tool which is used to create resources.

#### __Requirements__
  * #### AWS account
  * #### Terraform
  * #### Visual studio code
  * #### All my commands were run on __git bash__

#### Terraform is downloaded as a binary package specific to your operating system, to install save in a preferred folder then copy file path to environment variable (this can be confusing at first).

#### Run __terraform version__ to see if terraform is properly installed (it should bring up a version).

#### Steps

#### 1. On vs code, configure provider (AWS in this case), in __main.tf__ file
![](images/tf4-hcl-config.png)
#### 2. Run __terraform init__ to initialize and install plugins required; after include provider region and version in main.tf file.
![](images/tf1-init.png)
#### 3. Login to your AWS account to create an IAM user, using programmatic access as access type.
![](images/tf2-iam-user.png)
#### 4. Create an S3 bucket on AWS, giving bucket a unique name.
![](images/tf3-s3-bucket.png)
#### 5. Before creating resources, we have to authenticate terraform to AWS provider, using the environment variables method (which involves exporting the access keys created from the IAM user given the programmatic access type), this method is safer and preferable.

#### Create resource using this format resource "aws_s3_bucket""my_terraform_bucket"{
 #### bucket = "bucket_kene"

#### }
![](images/tf4-hcl-config.png)
#### 6. Run __terraform plan__ command to create an execution plan, it gives details of what terraform will do when a command is executed.
![](images/tf5-plan.png) </br></br>
![](images/tf6-plan2.png)
#### 7. Run __terraform apply__ command to execute the action stated in the  plan, it also generates the plan and asks if we want to perform the actions (it performs the action if we specify, yes).

![](images/tf7-apply.png)</br></br>
![](images/tf8-apply1.png)
#### 8. Notice the bucket specified earlier has been created on AWS, 
![](images/tf9-s3-bucket-new.png)
#### 9. Using the terraform apply command, terraform recognized that no change has been made after refreshing state.
![](images/tf10-apply-refresh.png)
#### 10. After apply command, it creates a __terraform.tfstate__, which contains details in JSON format
![](images/tf-10-1-tfstate.png)

#### __Terraform has what is called states namely: desired state, known state and actual state__.
#### Desired state - is the actual state we want to create using terraform.
#### Known state -is stored in the terraform.tfstate, it is the state of the previous execution, which acts as a backup.
#### Actual state- this is the state in the cloud

#### 11. To see how states work in terraform, I edit my bucket name (which is my desired state) and run terraform apply again, notice that it refreshes the state using the id gotten from the known state (previous execution), then recognizing that it is not the same with known state, it replaces the old bucket name in the actual state with the new bucket name  
![](images/tf11-editname.png)
#### 12. It shows that one resource is destroyed(old bucket name) and one is added(new bucket name).
![](images/tf11-editname-1.png)
#### 13. Notice that he name has been edited on AWS (which is our actual state)
![](images/tf11-s3-editname.png)
#### 14. On main.tf, I updated the version from false to true and ran terraform apply, using the concept of state, terraform was able to recognize the change before updating.
![](images/tf12-version.png)
![](images/tf12-version1.png)
#### 15. Using __terraform console__ command, we can view output on the console (you can leave the console using __exit__)
![](images/tf13-console.png)
#### 16. Or viewed by declaring output on __main.tf file__
![](images/tf14-output.png)
#### 17. Create 2 IAM users by declearing on the main.tf file
![](images/tf15-iam.png) </br></br>
![](images/tf15-iam1.png)
#### 18. IAM user created on terraform, visible on AWS
![](images/tf15-iam2.png)
#### 19. __terraform destroy__ command destroys all the resources being managed by the current working directory, it deletes the resources from AWS.
![](images/tf16-destroy.png)</br></br>
![](images/tf16-destroy1.png)
#### 20. This is the whole code to create IAm users and S3 buckets, they can be split into different files for clarity (eg. the resource bit in one file and the output bit in a seperate file).
![](images/tf17.png)

#### __Note that if you have issues creating your resources on terraform, check that your resource name is unique (example bucket name) and you are using the correct access keys__.

