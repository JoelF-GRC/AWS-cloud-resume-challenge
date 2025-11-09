# Cloud Resume Challenge – Project Plan

This document outlines the plan and progress for my **AWS Cloud Resume Challenge**, which I adapted into an art and professional portfolio site.

---

## Objectives

- Build a **static, responsive website** hosted entirely on AWS.
- Feature my **artwork and professional background** in a clean, modern design.
- Implement a **serverless visitor counter** using Lambda, API Gateway, and DynamoDB.
- Apply **security and GRC best practices** across all AWS resources.
- Automate deployment through **CI/CD** and Infrastructure as Code.

---

## AWS Services

| Service | Role |
|----------|------|
| S3 | Host static HTML, CSS, and image assets |
| CloudFront | Provide HTTPS, caching, and global delivery |
| Lambda | Backend logic for the visitor counter |
| API Gateway | Public endpoint to trigger Lambda |
| DynamoDB | Store visitor count data |
| IAM | Manage access control using least privilege |
| CloudWatch | Log and monitor system activity |
| CloudTrail | Capture audit logs for governance and visibility |

---

## Deliverables

- Functional front-end site (art galleries + professional page)
- Working visitor counter (Lambda + DynamoDB)
- Infrastructure-as-Code template for backend services
- CI/CD pipeline via GitHub Actions
- Security and GRC documentation with control mapping

---

## Week-by-Week Progress

### Week 1
- Defined architecture and services.
- Created diagram and project folder structure.
- Drafted this plan and initial GRC considerations.

### Week 2
- Built and tested HTML/CSS locally.
- Set up Lambda, DynamoDB, and API Gateway.
- Deployed S3 + CloudFront stack and tested delivery.

### Week 3 (Planned)
- Connect visitor counter API.
- Finalize CI/CD integration.
- Begin documenting CRC requirement mapping in `/docs/site-implementation.md`.

---

## Notes

- The project is designed to remain within the **AWS Free Tier** using S3, CloudFront, Lambda, DynamoDB, and API Gateway.  
- Each service is configured with **encryption, logging, and least-privilege IAM roles** for security and compliance.

---

**Joel Flood**  
San Diego, CA  
[LinkedIn](https://www.linkedin.com/in/joelflood/) | [GitHub](https://github.com/JoelF-GRC)
