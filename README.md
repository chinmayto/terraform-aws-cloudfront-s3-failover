# Deploying a cloudfront distribution with Multiple Origin for S3 Static Website using terraform
Deploying a cloudfront distribution with Multiple Origin for S3 Static Website using terraform

You can set up CloudFront with origin failover for scenarios that require high availability. We can create an origin group with two origins: a primary and a failover. If the primary origin is unavailable, or returns specific HTTP response status codes that indicate a failure, CloudFront automatically switches to the failover origin.

CloudFront routes all incoming requests to the primary origin, even when a previous request failed over to the secondary origin. CloudFront only sends requests to the secondary origin after a request to the primary origin fails.

### Architecture Diagram:

![alt text](/images/diagram.png)

![alt text](/images/diagram2.png)

### Step 1: Create a primary and failover S3 Buckets with unique name and host static website by uploading files

### Step 2: Create a cloudfront distribution with primary and failover origin

### Step 3: Update S3 Bucket policy to allow access from cloudfront 

### Terraform Apply Output:
```
Apply complete! Resources: 9 added, 0 changed, 0 destroyed.

Outputs:

cloudfront_domain_name = "http://d1rwkmekbjnbkd.cloudfront.net"
```

S3 Buckets

![alt text](/images/s3buckets.png)

CloudFront Distribution:

![alt text](/images/cfdist.png)

CloudFront Distribution Origin as S3 primary and failover and origin group

![alt text](/images/origin1.png)

![alt text](/images/origin2.png)

S3 Bucket Policy to allow access from cloudfront - primary and failover bucket

![alt text](/images/bucketpolicy1.png)

![alt text](/images/bucketpolicy2.png)

Using cloudfront domain name to access S3 static website

![alt text](/images/s3primarywebsite.png)

Failover to S3 failover bucket by removing s3 primary bucket policy manually from console (after TTL timeout)

![alt text](/images/s3failoverwebsite.png)

### Terraform Destroy Output:
```
Destroy complete! Resources: 9 destroyed.
```

### Resources:

AWS CloudFront: https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/Introduction.html

AWS CloudFront Origin Failover: https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/high_availability_origin_failover.html

