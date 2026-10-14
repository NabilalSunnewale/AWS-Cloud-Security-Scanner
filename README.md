# AWS-Cloud-Security-Scanner
# Automated Cloud Storage Malware & DLP Scanner
🚧 **Status:** Active Development & Cloud Deployment in Progress.

## Overview
A serverless DevSecOps pipeline built on AWS to automatically scan incoming S3 objects for malware and sensitive data leaks (Data Loss Prevention) using Python, AWS Rekognition (OCR), and the VirusTotal API.

## Core Architecture
- **Event Source:** Amazon S3 (ObjectCreated trigger)
- **Compute:** AWS Lambda (Serverless Python 3 execution)
- **Malware Intelligence:** VirusTotal v3 API (In-memory SHA-256 validation)
- **Data Loss Prevention (DLP):** AWS Rekognition (Image OCR) & Python Regex (Credentials/Credit Cards)
- **Alerting & Routing:** Amazon SNS for admin notifications and automated isolation to Quarantine Buckets.

## Workflow
1. User uploads a file (.txt, .jpg, .png) to the `Upload Bucket`.
2. S3 triggers the Lambda function automatically.
3. Lambda calculates the file's hash and checks for malware signatures via VirusTotal.
4. If an image, AWS Rekognition extracts embedded text. Regex scans for exposed AWS IAM keys or credit card patterns.
5. If clean -> Moved to `Clean Bucket`. If threat detected -> Moved to `Quarantine Bucket` and SNS alert dispatched.
