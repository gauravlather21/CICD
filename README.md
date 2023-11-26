# Create and configure a Static Website With S3 And CloudFront
During this project, you will host your static website using the Amazon Simple Storage Service (S3) so that it is secure, fast, protected against data loss, and can scale to support enterprise-level traffic. To do that, you'll store your website files on Amazon S3 and also use S3 to deliver your content to visitors to your website.

After setting up the static website on S3, this project will show you how to use Amazon CloudFront to create a content delivery network (CDN). A CDN makes your website content available from data centers around the world, called edge locations. Using edge locations improves the speed of your website by reducing latency. Doing so is especially important if your website displays large media files such as high-resolution images, audio, or video.

## Project Objectives
* Configure static website hosting on Amazon S3
* Configure static websites to work with CloudFront distributions
## Prerequisites
* Creating and navigating S3 buckets
* Creating CloudFront distributions

## Step 1: Logging In to the Amazon Web Services Console
login to your AWS account using your credentials.

## Step 2: Creating an Amazon S3 Bucket for a Static Website
1. In the AWS Management Console search bar, enter S3, and click the S3 result under Services:

2. To start creating a new Amazon S3 bucket, in the top-right, click Create bucket:

3. Under General configuration, enter the following:
Bucket name: Enter 
* demo-bucket-<UniqueNumber> (Append a unique number to the end of calabs-bucket-)
* Region: Ensure US West (Oregon) us-west-2 is selected

You have added a unique number to the bucket name because Amazon S3 bucket names must be unique regardless of the AWS region in which the bucket is created.

4. Make sure to select ACLs Enabled:

5. In the Block Public Access section, un-check the Block all public access check box:

6. To acknowledge that you want to make this bucket publicly accessible, check I acknowledge that the current settings might result in this bucket and the objects within becoming public:

7. To finish creating your Amazon S3 bucket, scroll to the bottom of the form and click Create bucket:

### Enable static website hosting for your bucket:

8. In the list, click the name of your bucket:

9. In the row of tabs under Bucket overview, click Properties:

The Properties tab allows you to enable and disable various Amazon S3 bucket features.

10. Scroll to the bottom of the Properties page and in the Static website hosting section, on the right, click Edit:

The Edit static website hosting form will load.

11. In the Static website hosting field, select Enable:

12. Enter the following, leaving all other fields at their defaults:
* Index document: Enter index.html
* Error document: Enter error/index.html

13. To finish enabling static website hosting, scroll to the bottom, and click Save changes:

Your Amazon S3 bucket is ready to host.
In this step, you created an Amazon S3 bucket and you configured it to host a static website.

In the next step, you will upload an example static website to your bucket and modify your bucket's permissions to allow access.

## Step 3: Uploading a Static Site to an Amazon S3 Bucket

### Set a bucket policy:
1. In the Amazon S3 console, in the row of tabs, click Permissions:

2. Scroll down to the Bucket policy section, and on the right, click Edit.

3. In the Policy editor, copy and paste the following and replace YOUR_BUCKET_NAME with the name of your S3 bucket:
```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "AddPerm",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::YOUR_BUCKET_NAME/*"
    }
  ]
}
```
This policy will allow public access to all objects in your S3 bucket.

4. To save your bucket policy, at the bottom of the page, click Save changes.

### Upload objects in s3 bucket:
5. In the row of tabs, click Objects.

6. To begin uploading the website to your Amazon S3 bucket, scroll down and click Upload:
7. In the Files and folders section, click Add files:
8. Using the file picker, select all files and folders from inside the [Website](/configure-static-website/Website/) folder.

_Note: ensure you upload all the files and folders inside it but not the Website folder itself. To be able to access the website, the index.html file must be at the top-level of your Amazon S3 bucket._

9. Scroll to the bottom of the page and click Upload.

10. To exit the Upload form, on the right, click Close.

### Test that your website is accessible:
11. To retrieve the endpoint for your bucket, click the Properties tab, scroll to the bottom, and click the copy icon next to the Bucket website endpoint:

12. Paste the endpoint into the address bar of a new browser tab.

You will see a website.

In this step, you created a bucket policy, uploaded an example website, and confirmed it was accessible publicly in a web browser.

AWS doesn't recommend serving websites directly from Amazon S3. Instead, they recommend using Amazon S3 as an origin for a Content Delivery Network (CDN). A CDN pulls copies of the site from the origin and stores them in multiple global locations. The main benefit of using a CDN is lower latency for users when they access the site.

In the next step, you will put your website behind a CDN by creating an Amazon CloudFront distribution.




































