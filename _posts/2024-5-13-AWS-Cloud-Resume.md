---
layout: post
title: AWS Cloud Resume Challenge
subtitle: Create and host a cloud resume website
gh-repo: https://github.com/kai-ion/aws-cloud-resume
gh-badge: [star, fork, follow]
tags: [AWS, Cloud, Web Development]
comments: true
---



# AWS-CLOUD-RESUME-CHALLENGE

This is a demo post to show you my progress in the [AWS Cloud Resume Challange](https://cloudresumechallenge.dev/docs/the-challenge/aws/)

What is Cloud Resume Challenge? - [The Cloud Resume Challenge](https://cloudresumechallenge.dev/) is a multiple-step resume project which helps build and demonstrate skills fundamental to pursuing a career in Cloud. The project was published by Forrest Brazeal.


**Services Used**:

- S3
- AWS CloudFront
- Certificate Manager
- AWS Lambda
- Dynamo DB
- GitHub Actions
- Terraform

## [Live Demo using github 🔗](https://kai-ion.github.io/aws-cloud-resume/)
## [Live Demo using AWS 🔗](https://cloudresume.kaiion.com/)

<br>

# Setup Tutorial

- [Static Website](#static-website)
- [Custom Domain](#custom-domain)
- [S3 Bucket](#s3-bucket)
- [Cloundfront](#cloudfront)
- [SSL Certificate](#ssl-certificate)
- [Route53 DNS Management](#route53-dns-management)
- [Javascript - Visitor Counter](#javascript---visitor-counter)
- [DynamoDB](#dynamodb)
- [AWS Lambda Function](#aws-lambda_function)
- [AWS Lambda Function connection](#aws-lambda_function-connection)
- [Git and CI/CD](#git-and-cicd)

<br>

## Static Website
I created my static website based on a template

![image](/assets/img/img-AWS-Cloud-Resume/website.PNG)

<br>

## Custom Domain

- I used namecheap to purchase one domain and then I also used AWS Route 53 to purchase a domain
    - https://www.namecheap.com/
    - https://aws.amazon.com/route53/ 
- You can see below that I purchased the domain kaiion.com on namecheap and piguit.com on Route 53

![image](/assets/img/img-AWS-Cloud-Resume/Namecheap.PNG)

![image](/assets/img/img-AWS-Cloud-Resume/Route53%20Domain.PNG)

<br>

## S3 Bucket
1. First you have to create an AWS account which is pretty straight forward
2. Log onto your AWS console, search and click on “S3”
3. Then click on the “Create bucket” button

![image](/assets/img/img-AWS-Cloud-Resume/S3%20bucket.webp)

4. When choosing a name for the bucket, there are a list of naming conventions on S3
    - Must be globally unique
    - Must be DNS-compliant, meaning they can only contain lowercase letters, numbers, periods (.), and hyphens (-)
    - Bucket names should not contain underscores (_), uppercase letters, spaces, or any special characters
    - Bucket names should be between 3 and 63 characters long
    - [Reference to the S3 doc for naming convention](https://docs.aws.amazon.com/AmazonS3/latest/userguide/bucketnamingrules.html?icmpid=docs_amazons3_console)
5. You can choose your region, I selected “us-east-1” as the region for the bucket, and leave all other settings as default

![image](/assets/img/img-AWS-Cloud-Resume/bucket-creation.PNG)

![image](/assets/img/img-AWS-Cloud-Resume/bucket-creation-2.webp)

6. Click on the “Create bucket” button at the bottom

![image](/assets/img/img-AWS-Cloud-Resume/bucket-creation-3.webp)

7. You will see your bucket created along with the corresponding message

![image](/assets/img/img-AWS-Cloud-Resume/bucket-creation-4.PNG)

8. Navigate into the created bucket and proceed to upload your static website files
    - Click on “Upload” button
    - Click on “Add files” to upload them into the bucket
    - Once the files appear in the bucket, click on the “Upload” button to proceed with the upload process
    - Our website is almost ready to be hosted

![image](/assets/img/img-AWS-Cloud-Resume/bucket-upload.PNG)

![image](/assets/img/img-AWS-Cloud-Resume/bucket-upload-2.PNG)

## Cloudfront

1. Go to CloudFront resource by navigating through the search bar.

![image](/assets/img/img-AWS-Cloud-Resume/cloudfront-1.webp)

2. Click on “Create distribution” button.

![image](/assets/img/img-AWS-Cloud-Resume/cloudfront-2.webp)

3. Select your s3 bucket domain in “Origin Domain” section.

![image](/assets/img/img-AWS-Cloud-Resume/cloudfront-3.PNG)

4. “Create new OAC” after selected “Origin access control settings (recommended)” in “Origin access” section.
    - Origin type could be “S3”.

![image](/assets/img/img-AWS-Cloud-Resume/cloudfront-4.PNG)

5. In Viewer protocol policy select “HTTPS only”.

![image](/assets/img/img-AWS-Cloud-Resume/cloudfront-5.PNG)

6. Scroll down to “Cache key and origin requests” and set next values.

![image](/assets/img/img-AWS-Cloud-Resume/cloudfront-6.PNG)

7. In my case I turn off WAF (Web Application Firewall) to save money

![image](/assets/img/img-AWS-Cloud-Resume/cloudfront-7.PNG)

8. Add /index.html to “Default root Object” field and click create distribution.

![image](/assets/img/img-AWS-Cloud-Resume/cloudfront-8.PNG)

9. When the distribution is created, you may receive a notification stating that The S3 bucket policy needs to be updated. In this case, click on the “Copy policies” button and add the copied policies to your S3 bucket’s policies.

![image](/assets/img/img-AWS-Cloud-Resume/cloudfront-9.PNG)

10. Open the S3 bucket you created earlier and navigate to the “Permissions” tab. Scroll down to the “Bucket Policies” section and click on the “Edit” button.
    - Paste your policies and click on “Save changes”

![image](/assets/img/img-AWS-Cloud-Resume/s3-bucket-policy.PNG)

![image](/assets/img/img-AWS-Cloud-Resume/s3-bucket-policy-2.PNG)

11. Go to your CloudFront distribution “Error pages” tab and create error responses for 403 and 404.

![image](/assets/img/img-AWS-Cloud-Resume/cloudfront-10.PNG)

![image](/assets/img/img-AWS-Cloud-Resume/cloudfront-11.PNG)

12. Back in the General tab, under Details section you can see a Distribution domain name, you can now copy and paste that link into your browser to see your website

![image](/assets/img/img-AWS-Cloud-Resume/cloudfront-12.PNG)

![image](/assets/img/img-AWS-Cloud-Resume/cloudfront-13.PNG)

## SSL Certificate

1. Navigate to AWS Certificate Manager (ACM) and select request
    - Click on “Next” and proceed to fill your domain name

![image](/assets/img/img-AWS-Cloud-Resume/SSL-1.PNG)

![image](/assets/img/img-AWS-Cloud-Resume/SSL-2.PNG)

2. In this case, I am requesting a wildcard certificate
    - A SSL/TLS Wildcard certificate is a single certificate with a wildcard character (*) in the domain name field. This allows the certificate to secure multiple sub domain names (hosts) pertaining to the same base domain.
    - For example, a wildcard certificate for *.(domainname).com, could be used for www.(domainname).com, mail.(domainname).com, store.(domainname).com, in addition to any additional sub domain name in the (domainname).com.

![image](/assets/img/img-AWS-Cloud-Resume/SSL-3.PNG)

3. For the validation method, I am using email validation because it is easier for me

![image](/assets/img/img-AWS-Cloud-Resume/SSL-4.PNG)

4. “Request” button to get your certificate
    - In my case I received an email to verify the SSL certificate
    - After awhile you should see the status changed to Issued

![image](/assets/img/img-AWS-Cloud-Resume/SSL-5.PNG)

5. Navigate back to your Cloudfront distribution to add the SSL certificate and alternate domain name (CNAME) record under general tab, section settings, and select edit
    - Add the alternate domain name you like
    - Add the SSL certificate
    - Select save changes

![image](/assets/img/img-AWS-Cloud-Resume/SSL-6.PNG)

![image](/assets/img/img-AWS-Cloud-Resume/SSL-7.PNG)

6. You should see that your cloudfront distribution settings updated with the new alternate domain names and custom ssl certificate

![image](/assets/img/img-AWS-Cloud-Resume/SSL-8.PNG)

## Route53 DNS management

1. Setup Route 53, Amazon’s DNS service

2. If you purchased the domain on NameCheap, you would have to set up and configure the necessary Name Server (NS) records on the NameCheap side
    - By seamlessly integrating Route 53 with Namecheap, we can efficiently manage our DNS settings and ensure proper routing of traffic to our hosted resources.

3. To begin, navigate to the Route 53 service in your AWS console and click on “Create hosted zone”. This will initiate the process of setting up a hosted zone where you can manage the DNS records for your domain.

![image](/assets/img/img-AWS-Cloud-Resume/DNS-1.webp)

4. Enter your domain name in the “Domain Name” field and click on “Create hosted zone”

![image](/assets/img/img-AWS-Cloud-Resume/DNS-2.webp)

5. To configure NS records in Namecheap, you need to copy the NS records from your hosted zone in Route 53 and update the DNS settings in your Namecheap account by replacing the existing NS records with the ones obtained from Route 53

![image](/assets/img/img-AWS-Cloud-Resume/DNS-3.webp)

6. Back in your NameCheap portal, in the “Domain List” section, click on “Manage” located on the right side, opposite to your domain.

![image](/assets/img/img-AWS-Cloud-Resume/DNS-4.webp)

7. In the “Nameservers” section of the Namecheap DNS management interface, select the option for custom DNS and enter your NS records.
    - Don’t forget to save your records click on green mark
    - We can verify this later using a website like dnschecker to confirm the correctness of the NS record configuration.

![image](/assets/img/img-AWS-Cloud-Resume/DNS-5.webp)

![image](/assets/img/img-AWS-Cloud-Resume/DNS-6.webp)

![image](/assets/img/img-AWS-Cloud-Resume/DNS-7.webp)

8. Next step is to create an A record in our hosted zone. Navigate to the hosted zone section in Route53 to proceed

![image](/assets/img/img-AWS-Cloud-Resume/DNS-8.webp)

9. Click on “Create Record”.
    - Input subdomain name if you have one
    - Record type is — A. Set Alias toggle, and select your distribution that you created above from the search field.
    - Click on “Create Record”.

![image](/assets/img/img-AWS-Cloud-Resume/DNS-9.webp)

10. Your website should be able to be reached at the record name, for my case it would be at cloudresume.piguit.com

11. You can add additional subdomains that points to this A record, for example you may want to enable www.cloudresume.piguit.com
    - Remember to add the additional certificate for each additional subdomains you want to your cloud distribution, with AWS ACM, you can add multiple certificates in one request
    - This step will take some time to load

![image](/assets/img/img-AWS-Cloud-Resume/DNS-10.webp)

## Javascript - Visitor counter

![image](/assets/img/img-AWS-Cloud-Resume/visitor-counter-home.PNG)

1. To set up a visitors counter, we need four things:
    - Javascript code to display the counter
    - Javascript API call to fetch the data from AWS DynamoDB
    - AWS Lambda function to update the table on DynamoDB


2. First create a script.js file in your website repository, and add the script to fetch data from aws and display it 
    - Leave the fetch url blank for now until we create the lambda function on aws

![image](/assets/img/img-AWS-Cloud-Resume/javascript-visitor-counter-1.PNG)

3. Add a reference to your scripts.js in your index.html file

![image](/assets/img/img-AWS-Cloud-Resume/javascript-visitor-counter-2.PNG)

4. Display the data in your html

![image](/assets/img/img-AWS-Cloud-Resume/javascript-visitor-counter-3.PNG)


## DynamoDB

1. Navigate to AWS Console and into DynamoDB services, select “Create Table”

![image](/assets/img/img-AWS-Cloud-Resume/visitor-counter-2.PNG)

![image](/assets/img/img-AWS-Cloud-Resume/visitor-counter-3.PNG)

2. Input a table name, then set the partition key to id. Then create table

![image](/assets/img/img-AWS-Cloud-Resume/visitor-counter-4.PNG)

3. Once the table is created, navigate to actions and explore items
    - Then select create item

![image](/assets/img/img-AWS-Cloud-Resume/visitor-counter-4.5.PNG)

![image](/assets/img/img-AWS-Cloud-Resume/visitor-counter-5.PNG)


4. Add a new item with attribute of numbers and name it views, and assign it a value of 1

![image](/assets/img/img-AWS-Cloud-Resume/visitor-counter-6.PNG)


## AWS Lambda_Function

1. Navigate to AWS Console and into Lambda Services, then select create a function

![image](/assets/img/img-AWS-Cloud-Resume/Lambda-1.PNG)

2. In the new window, give your lambda function a name, I named mine cloudresume-api

3. Then set the default execution role to “Create a new role”

![image](/assets/img/img-AWS-Cloud-Resume/Lambda-2.PNG)

4. In the advanced settings, Check in Enable function URL so the function can be accessed via a URL and set auth type to NONE allowing everyone access to the function. Then check in Configure cross-origin resource sharing

5. Then select create function

![image](/assets/img/img-AWS-Cloud-Resume/Lambda-3.PNG)

6. In the newly created function, you will be able to see a Function URL, which after you navigate to on your browser, you can see Hello from lambda displayed

![image](/assets/img/img-AWS-Cloud-Resume/Lambda-4.PNG)

![image](/assets/img/img-AWS-Cloud-Resume/Lambda-5.PNG)

7. Now we edit the code in the lambda function to display our view count

    - You can copy and paste my code from: https://github.com/kai-ion/aws-cloud-resume/blob/main/Lambda-function/lambda_function.py

    - Remember to set the correct table name and the table item Ids

![image](/assets/img/img-AWS-Cloud-Resume/Lambda-6.PNG)

8. Test if there is any bug with ur function and then select Deploy 

9. You should be able to view the visitor count in the aforementioned lambda URL

![image](/assets/img/img-AWS-Cloud-Resume/Lambda-7.PNG)

10. Now we can add this function url to our JS code in the previous step

![image](/assets/img/img-AWS-Cloud-Resume/visitor-counter-1.PNG)

## AWS Lambda_function connection

1. Setup lambda function to get the records from dynamoDB, go to the function and navigate to the configuration tab and then the permission tab

![image](/assets/img/img-AWS-Cloud-Resume/Lambda-permission-2.PNG)

2. Click on the role under Role name to open an IAM window, then click add permissions under permissions tab, and select attach policy

![image](/assets/img/img-AWS-Cloud-Resume/Lambda-permission-1.PNG)

3. In the search bar, look up dynamoDB, then add the policy needed. In my case I added full access permission

![image](/assets/img/img-AWS-Cloud-Resume/Lambda-permission-3.PNG)


## Git and CI/CD

1. Create a github repo and upload all the website files to the repo

2. Now we have to setup github actions by creating a directory called .github/workflows

    - Inside of it, we will create a file called front-end-cicd.yml

![image](/assets/img/img-AWS-Cloud-Resume/CICD-1.PNG)

3. You can paste my code: [link](https://github.com/kai-ion/aws-cloud-resume/blob/main/.github/workflows/front-end-cicd.yml)

    - In the code, we use the steps checkout and sync from github actions and jakejarvis to checkout from github and sync it to our aws s3 bucket

4. After you push the new codes onto github, you have to setup your secrets or access keys to your aws profile
    - Log onto aws and set up a new user and give it the access type you want
    - Keep note of the keys

5. Next we go back to github and add the keys in secrets and variables in settings
    - Now the build should be successful and your repo and s3 bucket should be sync up

![image](/assets/img/img-AWS-Cloud-Resume/CICD-2.PNG)

# Thats all, You’re all set up!





