# AWS S3 Static Website with CloudFront

## Overview
This project demonstrates how to host a static website using Amazon S3 and distribute it securely using CloudFront.

The project includes S3 static website hosting, CloudFront distribution, IAM permissions, and troubleshooting common errors such as Access Denied (403).

---

## Architecture
User → CloudFront → S3

![Architecture](./architecture/architecture-diagram.png)

---

## Services Used
- Amazon S3
- Amazon CloudFront
- AWS IAM

---

## Project Structure
aws-s3-static-website
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
│
└── README.md

---

## Setup Steps

### 1. Create S3 Bucket
Create an S3 bucket and upload the website files.
![S3 Bucket](<screenshots/S3 Screenshots/S3 static website files.PNG>)

### 2. Enable Static Website Hosting
Enable static website hosting in the S3 bucket properties.
![Static Hosting](<screenshots/S3 Screenshots/Enable-static-website-hosting-in-the-S3-bucket-properties..PNG>)

### 3. Configure Public Access
Disable Block Public Access and configure bucket policy.
![Public Access](<screenshots/S3 Screenshots/Disable-Block-Public-Access-and-configure-bucket-policy..PNG>)

### 4. Create CloudFront Distribution
Create a CloudFront distribution pointing to the S3 bucket.
![CloudFront Distribution](<screenshots/S3 Screenshots/CloudFront-Distribution.PNG>)

### 5. Access Website via CloudFront
Access the website using the CloudFront domain name.
![Website Working](./screenshots/cloudfront/domain-working.png)

---

## Problems and Solutions

### Problem 1 – Access Denied (403)
When accessing the website, a 403 Access Denied error appeared.
![403 Error](./screenshots/s3/403-error.png)

**Cause:**
The S3 bucket was blocking public access.

**Solution:**
- Disabled Block Public Access
- Added bucket policy to allow public read access

![Solution](./screenshots/solutions/fix-403.png)

**What I Learned:**
Understanding S3 permissions and public access settings is critical when hosting static websites.

---

## What I Learned
- How to host a static website using Amazon S3
- How CloudFront works as a CDN
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

---

## Author
Nahuel Egidi
