# aws-s3-static-website
# AWS S3 Static Website

## Overview
This project demonstrates how to host a static website using Amazon S3 and distribute it using CloudFront.

## Architecture
User → CloudFront → S3

## Services Used
- Amazon S3
- Amazon CloudFront
- AWS IAM

## Project Structure

aws-s3-static-website
│
├── website/
│   ├── index.html
│   ├── style.css
│   └── error.html
│
├── screenshots/
│
├── architecture/
│
└── README.md

## Problems and Solutions

###Problem 1 - Access Denied
![Access Denied](./screenshots/403%20Denied%20Forbidden.PNG)

## What I Learned
###Problem 1 - Access Denied
Always pay attention to the Bucket setting and allow public access.

## Future Improvements
