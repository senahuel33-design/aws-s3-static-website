# AWS S3 Static Website with CloudFront

## Overview
This project demonstrates two different ways to host a static website using Amazon S3 and distribute it using CloudFront:

1. Using S3 Static Website Endpoint (Public Bucket)
2. Using S3 REST API with CloudFront Origin Access Control (Private Bucket – Recommended)

The project also includes IAM permissions and troubleshooting common errors such as Access Denied (403).

---

## Architecture

### Architecture 1 – Public S3 Website Endpoint
User → CloudFront → S3 Website Endpoint (Public Bucket)

![Architecture Public](<4 - Architecture/architecture-public.PNG>)

### Architecture 2 – Private S3 with OAC (Recommended)
User → CloudFront → Origin Access Control → S3 (Private Bucket)

![Architecture Private](<4 - Architecture/architecture-private.png>)
---

## Services Used
- Amazon S3
- Amazon CloudFront
- AWS IAM

---

## Project Structure

aws-s3-static-website/
│
├── terraform/
│   ├── main.tf
│   ├── variables.tf
│   └── outputs.tf
│
├── website/
│   ├── index.html
│   ├── style.css
│   └── error.html
│
├── screenshots/
│   ├── s3/
│   ├── cloudfront/
│   └── solutions/
│
├── architecture/
│   ├── architecture-public.png
│   └── architecture-private.png
│
└── README.md

---

## Setup Steps

### 1. Create S3 Bucket
Create an S3 bucket and upload the website files.
![S3 Bucket](<3 - Screenshots/S3 Screenshots/S3 static website files.PNG>)

### 2. Enable Static Website Hosting
Enable static website hosting in the S3 bucket properties.
![Static Hosting](<3 - Screenshots/S3 Screenshots/Enable-static-website-hosting-in-the-S3-bucket-properties..PNG>)

### 3. Configure Public Access
Disable Block Public Access and configure bucket policy.
![Public Access](<3 - Screenshots/S3 Screenshots/Disable-Block-Public-Access-and-configure-bucket-policy..PNG>)

### 4. Access Website via S3 Website Endpoint
Access the website using the S3 static website endpoint URL.
![S3 Website](<3 - Screenshots/S3 Screenshots/Access-Website-via-S3-Website-Endpoint.PNG>)

### 5. Create CloudFront Distribution (Website Endpoint)
Create a CloudFront distribution pointing to the S3 bucket.
![CloudFront Distribution](<3 - Screenshots/CloudFront/CloudFront-Distribution.PNG>)

### 6. Access Website via CloudFront
Access the website using the CloudFront domain name.
![Website Working](<3 - Screenshots/CloudFront/Access-Website-via-CloudFront.PNG>)

# Part 2 – Static Website Using CloudFront OAC (Private Bucket – Recommended)

### 1. Create Private S3 Bucket
Create a new S3 bucket and keep Block Public Access enabled so the bucket remains private.
![Private Bucket](<3 - Screenshots/CloudFront/Create Private S3 Bucket.PNG>)

### 2. Upload Website Files
Upload the website files (index.html, style.css, error.html) to the private S3 bucket.
![Upload Files](<3 - Screenshots/S3 Screenshots/S3 static website files.PNG>)

### 3. Create CloudFront Distribution
Create a CloudFront distribution and use the S3 REST API endpoint as the origin.
![CloudFront REST](<3 - Screenshots/CloudFront/CloudFront-Distribution.PNG>)

### 4. Configure Origin Access Control (OAC)
Create and attach an Origin Access Control so CloudFront can securely access the private S3 bucket.
![OAC](<3 - Screenshots/CloudFront/Configure-Origin-Access-Control-(OAC).PNG>)

### 5. Update Bucket Policy
Update the S3 bucket policy to allow access only from CloudFront, keeping the bucket private.
![Bucket Policy](<3 - Screenshots/CloudFront/New-CloudFront-policy-to-the-S3-bucket-policy.PNG>)

### 6. Configure Custom Error Pages
Configure CloudFront custom error responses so index.html loads correctly when accessing the root URL.
![Error Pages](<3 - Screenshots/CloudFront/Configure-Custom-Error-Pages.PNG>)

### 7. Access Website via CloudFront
Access the website securely using the CloudFront domain name.
![CloudFront Website](<3 - Screenshots/CloudFront/Access-Website-via-CloudFront.PNG>)

---

## Architecture Comparison

| Feature | S3 Website Endpoint | CloudFront + OAC |
|--------|--------------------|------------------|
| Bucket Public           | Yes | No |
| Security                | Low | High |
| Recommended              | No | Yes |
| Supports HTTPS| Via CloudFront | Yes |
| Production Ready         | No | Yes |

## Problems and Solutions

### Problem 1 – Access Denied (403)
When accessing the website, a 403 Access Denied error appeared.
![403 Error](<screenshots/S3 Screenshots/S3 Mistakes/403 Denied Forbidden.PNG>)

**Cause:**
The S3 bucket was blocking public access.

### Solution 1 - Access Denied (403)
- Disabled Block Public Access
- Added bucket policy to allow public read access

![Solution](<screenshots/S3 Screenshots/Disable-Block-Public-Access-and-configure-bucket-policy..PNG>)

**What I Learned:**
Understanding S3 permissions and public access settings is critical when hosting static websites.

### Problem 2 – Access Denied (403) (CloudFront)

### Solution 2 - Access Denied (403) (CloudFront)
 - S3 bucket policy fixed, I linked the new CloudFront policy to the S3 bucket policy
   ![Solution](<screenshots/S3 Screenshots/Solution/New-CloudFront-policy-to-the-S3-bucket-policy.PNG>)
 - Wrong Origin settled in CloudFront
   ![Solution](<screenshots/S3 Screenshots/Solution/Unnecessary-origin-deleted.PNG>)

**Cause:**

**What I Learned:**

**Solution:**
---

## What I Learned
- How to host a static website using Amazon S3
- Difference between S3 Website Endpoint and S3 REST API
- How CloudFront works as a CDN
- How to configure Origin Access Control (OAC)
- How to configure S3 bucket policies
- Troubleshooting Access Denied errors
- Basic AWS architecture design
- Importance of IAM and permissions
---

## Future Improvements
- Add HTTPS using ACM
- Add custom domain with Route 53
- Implement CI/CD deployment
- Add logging and monitoring
- Use Terraform to automate infrastructure


**Conclusion:**
The recommended architecture is using CloudFront with Origin Access Control and a private S3 bucket.


