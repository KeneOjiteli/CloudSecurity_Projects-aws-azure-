# HOW TO ENABLE VERSIONING IN AWS

#####  __Bucket Versioning__ on __Amazon S3__ is recommended to help protect against unintentionally overwriting or accidental deletion of objects; This service ensures that if someone accidentally performs a delete request on an object, it will not be deleted. Instead, a delete marker will be added. You can then delete this marker to recover the object. You should also consider setting a bucket policy so that not all users can perform delete requests. <br/><br/>

##### Steps.

##### 1. Login to your AWS account.
##### 2. Navigate to S3 and create a bucket (mine is named __versioningbucketkene__, as bucket names should be unique), enable __bucket versioning__.
![](versioning-images/v1.png)
##### 2. Upload a file (object) in bucket.
![](versioning-images/v2.png)
##### 3. To make my text file visible, I have to uncheck block public access (note that this is not best practice, just for learning purposes, as I can download and view the file).
![](versioning-images/v3.png)
##### 4. Confirming that I am unchecking public access.
![](versioning-images/v4.png)<br/><br/>
![](versioning-images/v5.png)
##### 5. Object is made public so as to be viewable on the browser (just for learning purposes).  
![](versioning-images/v6.png) <br/><br/>
![](versioning-images/v7.png)
##### 6. I modified the file and re-uploaded, toggle the __show versions__ switch, notice that I have 2 text files of different sizes (these are the multiple versions of the file). If the toggle switch is off, only the latest version is visible.
![](versioning-images/v8.png)
##### 7. To view any file, i have to make it public.
![](versioning-images/v9.png)
##### 8. Say, I delete a file by mistake (by clicking the delete button and typing delete for confirmation) .
![](versioning-images/v10delete.png)
##### 9. Notice there are no files.
![](versioning-images/v11.png)
##### 10. To view files toggle the show versions switch; Notice the __delete marker__ (to recover the file, delete the delete marker).
![](versioning-images/v12.png)
##### 11. Type __permanently delete__ to confirm deletion.
![](versioning-images/v13.png)
##### 12. After deletion of delete marker, the latest version of the file is visible.
![](versioning-images/v14.png)
##### 13. To view all versions, simply turn on the show versions switch.
![](versioning-images/v15.png)

##### 14. Files can also be permanently deleted by clicking delete and typing permanently delete to confirm deletion.

##### __Note that Cost will be higher with versioning turned on because there will be several versions of an object (file).__
