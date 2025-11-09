# AWS Cloud Resume Challenge – Art & Professional Portfolio

This project is my implementation of the **AWS Cloud Resume Challenge**, adapted into a personal website that combines an art portfolio** with a professional resume page.  
The goal is to demonstrate end-to-end use of AWS cloud services while creating something personal, creative, and technically sound.

---

## Overview

I’m building a responsive, static website hosted entirely in the AWS ecosystem.  
It highlights my artwork across multiple decades and includes a dedicated page for my professional background in **security, governance, risk, and compliance (GRC)**.

The site consists of:
- **Art portfolio pages** organized by decade (1990s–2020s) and medium.
- A **Professional** page that includes my resume and links to LinkedIn and GitHub.
- A **serverless visitor counter** using Lambda, DynamoDB, and API Gateway.
- **CI/CD automation** for continuous deployment.
- Documentation that ties technical implementation to **security and GRC principles**.

---

## Architecture Summary

The project follows a standard CRC architecture using AWS managed services:

| Layer | AWS Service | Purpose |
|--------|--------------|----------|
| Frontend | **S3** | Host static HTML, CSS, and image assets |
| Delivery | **CloudFront** | Provide HTTPS, global distribution, and caching |
| Backend | **API Gateway + Lambda** | Handle visitor counter logic |
| Database | **DynamoDB** | Store visitor count data |
| Access & Logging | **IAM, CloudWatch, CloudTrail** | Security, monitoring, and auditing |
| CI/CD | **GitHub Actions** | Automate deployment to S3 and CloudFront invalidation |

All services are configured with encryption, logging, and least-privilege IAM policies.  
The entire deployment stays well within AWS Free Tier limits.

---

## Repository Structure

```text
cloud-resume-challenge/
├── README.md                 # Project overview
├── crc-plan.md               # Project plan and progress notes
├── diagrams/
│   └── architecture.png      # Architecture diagram
├── infrastructure/           # IaC templates for backend services
│   └── visitor-counter.yml
├── resume-site/              # Static website
│   ├── index.html
│   ├── about.html
│   ├── 1990s.html
│   ├── 2000s.html
│   ├── 2010s.html
│   ├── 2020s.html
│   ├── digital-media.html
│   ├── professional.html
│   └── assets/
│       ├── css/style.css
│       └── images/
└── docs/
    └── site-implementation.md  # CRC requirements and validation notes
```

---

## Goals

- Build and host a modern, responsive portfolio site on AWS.  
- Apply **serverless architecture** for scalability and low cost.  
- Implement **secure deployment and governance practices** aligned with ISO 27001 and NIST CSF principles.  
- Document architecture, design choices, and operational controls.  
- Use **CI/CD** to make the site fully automated from GitHub to S3.  

---

## Progress Snapshot

- **Week 1:** Planned architecture, defined AWS services, created diagrams and base folder structure.  
- **Week 2:** Developed and tested site locally, configured S3 + CloudFront, and began backend setup (Lambda + DynamoDB).  
- **Week 3:** Connect visitor counter, complete CI/CD pipeline, and document implementation in `/docs`.  

---

## Local Testing

```bash
git clone https://github.com/JoelF-GRC/aws-cloud-resume-challenge.git
cd aws-cloud-resume-challenge/resume-site
open index.html
```

Once the API Gateway endpoint is live, update the `fetch()` URL in `index.html` to link the visitor counter to the deployed backend.

---

## Security & GRC Highlights

This project treats security as a design requirement, not an afterthought.

- S3 and DynamoDB encrypted by default.  
- IAM roles restricted to least privilege.  
- CloudFront serves content via HTTPS only.  
- CloudTrail and CloudWatch log key activity.  
- CI/CD process maintains version control and traceability.

These practices map naturally to frameworks like **ISO 27001**, **SOC 2**, and **NIST CSF**, and reflect the same controls I apply in my professional work.

---

## References

- [Cloud Resume Challenge – AWS](https://cloudresumechallenge.dev/docs/the-challenge/aws/)
- [AWS Well-Architected Framework](https://aws.amazon.com/architecture/well-architected/)
- [Amazon S3 Static Website Hosting](https://docs.aws.amazon.com/AmazonS3/latest/dev/WebsiteHosting.html)
- [AWS Serverless Application Model (SAM)](https://aws.amazon.com/serverless/sam/)

---

**Joel Flood**  
San Diego, CA  
[LinkedIn](https://www.linkedin.com/in/joelflood/)
