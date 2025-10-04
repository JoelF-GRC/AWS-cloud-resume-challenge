# AWS-cloud-resume-challenge

[![AWS](https://img.shields.io/badge/AWS-Cloud-orange)](https://aws.amazon.com/)
![Project](https://img.shields.io/badge/Project-Hands--on-blue)


## Project Overview
The **Cloud Resume Challenge (CRC)** is a hands-on AWS project designed to showcase cloud architecture, serverless deployment, CI/CD automation, and security/GRC best practices.  

This project demonstrates the following skills:  
- AWS Services: S3, CloudFront, Lambda, DynamoDB, API Gateway, IAM  
- Infrastructure as Code (IaC) using CloudFormation or Terraform  
- CI/CD pipelines via GitHub Actions / AWS CodePipeline  
- Logging, monitoring, and security controls (CloudTrail, CloudWatch, IAM)  
- GRC awareness: optional mapping to ISO 27001 / NIST CSF controls  

---

## Live Demo
Check out the deployed resume site here:  
**TBD**

---

## Architecture Diagram
![Architecture Diagram](./diagrams/architecture.png)  

**Highlights:**  
- Static resume hosted on S3  
- CloudFront distribution for global caching and HTTPS  
- Serverless Lambda function for visitor analytics  
- DynamoDB for storing visitor counts  
- CI/CD pipeline for automated deployment  
- CloudTrail and CloudWatch for monitoring and auditing  

---

## Week-by-Week Build Summary

| Week | Focus | Deliverables |
|------|-------|-------------|
| 1 | Planning & Architecture | `crc-plan.md` with project plan and diagram |
| 2 | Static Website Deployment | `crc-deployment.md`, S3 + CloudFront setup |
| 3 | Serverless Backend & Analytics | `crc-lambda.md`, Lambda + DynamoDB integration |
| 4 | CI/CD & Automation | `crc-cicd.md`, GitHub Actions / CodePipeline workflow |
| 5 | Security & GRC Integration | `crc-security.md`, IAM policies, logging, compliance mapping |
| 6 | Wrap-Up & Portfolio Polish | README.md, finalized diagrams, lessons learned |

---

## Security & GRC Highlights
- **IAM Least Privilege:** Roles and policies scoped to minimum necessary permissions  
- **Logging & Monitoring:** CloudTrail for auditing, CloudWatch for metrics/alerts  
- **Data Protection:** Optional KMS encryption for sensitive data  
- **Compliance Mapping:** Services mapped to ISO 27001 / NIST CSF where applicable  

---

## CI/CD & Infrastructure as Code
- **CI/CD:** GitHub Actions / AWS CodePipeline automates deployments  
- **IaC:** Templates stored in `/infrastructure` for reproducible builds  
- **Automation Highlights:**  
  - Automatic S3 bucket deployment  
  - Lambda function deployment with versioning  
  - DynamoDB table provisioning  

---

## Lessons Learned & Next Steps
- Insights on serverless architecture, IAM best practices, and secure deployment  
- Optional enhancements:  
  - Add Cognito authentication  
  - Backup/restore for DynamoDB  
  - Additional security controls or compliance mappings  

---

## Related Projects
- [AWS GRC Portfolio](https://github.com/JoelF-GRC/aws-sa-grc-portfolio) – SAA-C03 + Governance, Risk, and Compliance documentation and examples  

---

## Contact
- **GitHub:** (https://github.com/JoelF-GRC) 


