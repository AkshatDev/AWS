---
tags:
  - basics
---

## S3 Security

### S3 Bucket Policy

-  It is a type of resource policy.
- Like identity policies but attached to a bucket.
- Resource policies provide resource perspective policies. With Identity policies you can control what that identity can access, with resource policies you can control who can  access that resource.
- With identity policies you cannot grant access to an identity that is not in your AWS account but since resource policies can reference any identities, you can allow or deny identities outside your AWS account.  
- Allow/Deny anonymous principals, identity policies cannot have nothing attached to them, they must be attached to an identity but bucket policies can reference all principals, even those not authenticated by AWS.
- **Anonymous Access**: If the policy's `Principal` element is set to `*`, it allows or denies access to everyone, which can include unauthenticated (anonymous) users. This is commonly used for making objects publicly readable (although this should be handled with care due to security implications).


Resource policies have one major difference when compared to identity policies, that is a principal. In resource policies you will always have a principal to which one or more statements apply, It is also a good way of differentiating between resource policy and identity policy.

**Bucket policies should be your default thought when granting anonymous access to objects in buckets.**

**There can only be one bucket policy on a bucket but that policy can have multiple statements.**

### Access Control Lists (ACLs)

It is used less often these days.
It is a sub-resource of that object or bucket.
They are legacy and AWS recommends bucket policies.
They are inflexible and only allow simple policies.

### Block Public Access

Because of people failing to fully understand AWS bucket policy model, there were some data leaks that happened. Because of this AWS came up with this relatively new feature that helps block all anonymous access i.e. anything outside that AWS account. **Block Public Access over rules bucket policies no matter what access is given to outside principals.** These can be set when you set up a bucket.


What is the main difference between S3 bucket policies and identity policies?:: S3 bucket policies are resource-based policies that can specify permissions for any principal, allowing or denying access to resources within the bucket, including
<!--SR:!2024-08-31,3,250-->

How can S3 bucket policies grant access to users from other AWS accounts?:: S3 bucket policies can specify a `Principal` element with the AWS account IDs or IAM roles from other accounts, thereby granting specified permissions to those external users.
<!--SR:!2024-08-31,3,250-->

Why are Access Control Lists (ACLs) considered inflexible compared to bucket policies?:: ACLs are legacy features that offer basic permissions management for S3 buckets and objects, such as read and write access, and do not support the complex, granular permissions that can be defined with bucket policies.
<!--SR:!2024-08-31,3,250-->

What does the Block Public Access setting do in AWS S3?:: Block Public Access provides settings that override permissions in S3 bucket policies and ACLs to block all public access, regardless of other permissions, helping to prevent accidental data exposure.
<!--SR:!2024-08-31,3,250-->

In what scenarios should you consider enabling the Block Public Access feature on an S3 bucket?:: Enable Block Public Access on all S3 buckets unless there is a specific, controlled need to allow public access, such as for hosting a publicly accessible website or distributing public content.
<!--SR:!2024-09-04,7,250-->

What can be configured in a bucket policy that cannot be configured in an identity policy?:: A bucket policy can allow or deny access to any principal, including anonymous users and users from other AWS accounts, which is not possible with identity policies that are bound to specific IAM identities.
<!--SR:!2024-08-31,3,250-->

How many bucket policies can one bucket have?:: Only one with multiple statements.
<!--SR:!2024-08-31,3,250-->



## Static Website Hosting

Things to remember 


You have to set an index document and an Error document.
Generally, domain name is auto generated but if you do want a custom domain name using R53, it should match your bucket name.


Scenarios that are perfect for s3 - Offloading and out-of-bound pages
S3 is likely to be much cheaper for the storage and delivery of any media than a compute service.


Offloading -

Out-of-bound pages -


## Object Versioning and MFA Delete


Object Versioning is **by default off in S3, once you enable it, it cannot be turned off it can only be suspended.**

Without versioning enabled, if you modify any object, the old object is removed and is replaced by the new one. In case of versioning, every time an update is done to any object, a new ID is created and is allocated to the updated object and the old object with the old ID is also saved. 

You have to be careful with this because if you have an object of size 5 GB and you update it 5 times, the total space that object now consumes is 25 GBs because all the versions are saved. 

The default object that is returned is the latest object with the latest ID. You can however, always request any version of object by providing the ID with it.

If you try to delete an object without specifying the id, what happens is S3 creates ID for that object called **delete marker**, behind the scenes, S3 does not really delete anything but hides the object using the delete marker. If you delete the delete marker then the object is returned to its active state with all the previous states.

To actually fully delete an object, you have to specify the ID that you want to delete and that specific object gets deleted.

If you delete the latest ID then the previous ID becomes the default latest.

**Suspending versioning does not actually delete the existing objects and all the versions of them, you still have to pay for the consumed space.**
### MFA Delete

If MFA delete is enabled, then to change bucket versioning state, you need MFA.
MFA is also required to delete any version of an object

How does S3 handle deletions when versioning is enabled?:: S3 places a delete marker on the latest version of the object, which hides the object from view. The object is not actually deleted until the delete marker or specific version ID is permanently removed.
<!--SR:!2024-08-31,3,250-->

What is the impact on storage when versioning is enabled in an S3 bucket?:: Storage usage can increase significantly as every update to an object results in a new version being saved, which cumulatively adds to the total storage used.
<!--SR:!2024-08-31,3,250-->

What does suspending versioning in an S3 bucket do?:: Suspending versioning stops the creation of new versions but does not delete existing versions; all previously stored versions remain and continue to incur storage costs.
<!--SR:!2024-08-31,3,250-->

## Performance optimization

### PUT upload
By default, when data is uploaded to S3, is it done using **PUT upload** (s3:PutObject). This is a single stream of data upload and the max allowed upload limit is 5 GB.

If the download for any reason fails, the upload has to start again from the beginning.

Since it is only 1 stream of upload, this method is not very reliable and is prone it failures.

### Multipart Upload
Break down data and then upload using multiple streams.
The **minimum** data size is 100MB for the entire object to be able to use multipart upload.
Max 10000 parts where each part is from 5MB to 5GB and the last part is called leftover which can be less than 5MB.
The advantage is that if each individual stream fails, it can fail without affecting other streams.

### S3 Accelerated Transfer
**Amazon S3 Transfer Acceleration** is a feature that enables faster, more secure transfers of files over long distances between your client and an S3 bucket. It leverages Amazon CloudFront’s globally distributed **edge locations** to accelerate uploads to S3.

### How S3 Transfer Acceleration Works:

- When you use S3 Transfer Acceleration, your data is routed to an AWS edge location over an optimized network path. From there, the data is forwarded directly to the S3 bucket over Amazon’s backbone network, which often results in increased transfer speed compared to regular internet transfer speeds.

### Key Features:

- **Global Edge Network**: Utilizes the AWS CloudFront edge network, which consists of 216 points of presence in 84 cities across 42 countries (as of last update). Data is first transferred to the nearest edge location and then travels to the S3 bucket over the AWS backbone network.
- **Performance**: Typically, users experience the most significant performance improvements when uploading across continents or to regions far from their own. The farther away the client is from the S3 bucket, the more noticeable the improvement.
- **Easy to Use**: To enable Transfer Acceleration on a bucket, you simply turn it on in the S3 bucket’s properties in the AWS Management Console. You then use a distinct endpoint URL to upload your files, which directs your transfers through AWS edge locations.

### Usage Considerations:

- **Costs**: There is an additional charge for using S3 Transfer Acceleration, based on the amount of data transferred to and from S3. Pricing varies depending on the source of the data transfer and the destination bucket region.
- **When to Use**: It is most beneficial for transferring large files over long distances. If your applications are already located near an S3 bucket (geographically), or if you are transferring small amounts of data, the benefits might be less noticeable, and the cost may not justify the speed improvement.

### Example Use Case:

Imagine you are a media company located in Australia, and you frequently upload large video files to an S3 bucket located in the US East (N. Virginia) region. By enabling S3 Transfer Acceleration, you could significantly reduce the time it takes to upload these files, improving productivity and reducing delays in content delivery.

This feature is particularly useful for scenarios involving regular transfers of large amounts of data across continents or from regions with less optimal internet connectivity to AWS regions.

What is the maximum file size for a single PUT upload to S3?:: The maximum file size for a single PUT upload to S3 is 5 GB.
<!--SR:!2024-08-31,3,250-->


How does multipart upload enhance the reliability of uploading large files to S3?:: Multipart upload enhances reliability by allowing individual parts of the upload to fail and be retried without affecting the entire upload, reducing the impact of interruptions on the upload process.
<!--SR:!2024-08-31,3,250-->


What is the minimum object size recommended for using multipart upload on S3?:: The minimum object size recommended for using multipart upload on S3 is 100 MB.
<!--SR:!2024-08-29,1,230-->

How does Amazon S3 Transfer Acceleration speed up file transfers?:: S3 Transfer Acceleration speeds up file transfers by routing data to an AWS edge location over an optimized network path, then transferring it directly to the S3 bucket via Amazon’s backbone network.
<!--SR:!2024-08-31,3,250-->


When should you consider using S3 Transfer Acceleration?:: S3 Transfer Acceleration should be considered when transferring large files over long distances, especially if the client is far from the S3 bucket, to leverage improved performance through AWS’s global edge network.
<!--SR:!2024-08-31,3,250-->

