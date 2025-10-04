# Cloud Resume Challenge – Week 1 Plan

## Project Overview
The goal of this project is to deploy my resume as a **static website on AWS**, incorporating serverless components, CI/CD automation, and security/GRC best practices.

### Objectives
- Deploy a static resume site on **S3** with **CloudFront** distribution for HTTPS
- Implement a **visitor counter** using **Lambda + DynamoDB**
- Automate deployments using **CI/CD**
- Apply **security best practices** and GRC considerations
- Document and map AWS services to relevant security/compliance controls

---

## AWS Services to be Used
| Service | Purpose |
|---------|---------|
| S3 | Host static resume website |
| CloudFront | CDN with HTTPS |
| Lambda | Serverless backend for visitor counter |
| DynamoDB | Store visitor analytics |
| API Gateway | Trigger Lambda functions |
| IAM | Roles and policies for secure access |
| CloudTrail | Logging and audit trails |
| CloudWatch | Monitoring and alerts |

---

## High-Level Architecture
- **Static resume** served from **S3**
- **CloudFront** for global distribution and HTTPS
- **Lambda function** triggered via **API Gateway** for visitor analytics
- **DynamoDB** table stores visitor counts
- **CloudTrail / CloudWatch** for logging and monitoring

*Include a diagram here: `diagrams/architecture.png`*

---

## Security & GRC Considerations
- **IAM Roles / Policies:** Use least privilege for all services
- **Logging & Monitoring:** Enable CloudTrail and CloudWatch for auditing
- **Data Protection:** Encrypt DynamoDB tables where applicable
- **Compliance Mapping (Optional):**  
  - S3 encryption & versioning → ISO 27001 A.8, A.12  
  - Logging → NIST CSF DE.CM-7  
  - IAM least privilege → ISO 27001 A.9  

---

## Week 1 Deliverables
- `crc-plan.md` with completed project plan, services table, security notes
- Initial **architecture diagram** saved in `diagrams/architecture.png`
- GitHub repo created with proper folder structure:
cloud-resume-challenge/
├─ README.md
├─ crc-plan.md
├─ resume-site/
├─ infrastructure/
└─ diagrams/

---

## Notes / Next Steps
- Review CRC documentation: [https://cloudresumechallenge.dev/docs/the-challenge/aws/](https://cloudresumechallenge.dev/docs/the-challenge/aws/)  
- Prepare AWS account and IAM user for Week 2  
- Sketch detailed architecture diagram  
- Outline CI/CD approach for Week 4

