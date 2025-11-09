# Cloud Resume Challenge – AWS Art & Professional Portfolio

This project implements the **AWS Cloud Resume Challenge (CRC)** with a personal creative twist.  
Instead of a simple resume page, the site showcases my artwork across multiple decades alongside a professional page highlighting my experience in security, governance, risk, and compliance (GRC).

The site is fully serverless, built on **Amazon S3, CloudFront, Lambda, DynamoDB, and API Gateway**, with **CI/CD automation** and a focus on secure, well-documented architecture.

---

## Project Overview

Goals:

- Deploy a **responsive, minimal gallery-style website** on AWS.
- Present my **art portfolio** (1990s → 2020s + Digital Media).
- Include a **Professional** section with my resume and LinkedIn/GitHub links.
- Implement a **serverless visitor counter** using Lambda + DynamoDB + API Gateway.
- Apply **security and GRC best practices**, documented in this repo.
- Use **Infrastructure as Code (IaC)** and **CI/CD** for reproducible deployments.

This design satisfies the core Cloud Resume Challenge requirements while functioning as a real portfolio.

---

## AWS Services Used

| Service | Purpose |
|----------|----------|
| **S3** | Host static HTML/CSS/JS content for the site |
| **CloudFront** | CDN distribution layer with HTTPS (ACM certificate) |
| **Lambda** | Backend logic for visitor counter |
| **API Gateway** | Public API that triggers the Lambda function |
| **DynamoDB** | Stores visitor count (primary key = `id` = `"home"`) |
| **IAM** | Defines least-privilege roles and policies |
| **CloudTrail** | Captures audit logs and API activity |
| **CloudWatch** | Monitors Lambda and API Gateway metrics and logs |

---

## Architecture

**High-level design:**

1. Static web files (`index.html`, gallery pages, CSS, JS) hosted in S3  
2. CloudFront serves the content globally with HTTPS and caching  
3. Lambda + API Gateway handle visitor count reads/writes  
4. DynamoDB stores total visitor count  
5. CloudWatch and CloudTrail provide observability and audit logging  

Architecture diagram (in repo):  
`diagrams/architecture.png`

---

## Site Structure

```text
resume-site/
├── index.html              # Landing page / gallery hub
├── about.html              # Bio & context
├── 1990s.html              # 1990s artwork
├── 2000s.html              # 2000s artwork
├── 2010s.html              # 2010s artwork
├── 2020s.html              # 2020s artwork (new)
├── digital-media.html      # Digital art & experiments
├── professional.html       # Resume & professional profile
└── assets/
    ├── css/
    │   └── style.css
    └── images/
        ├── highlights/
        ├── 1990s/
        ├── 2000s/
        ├── 2010s/
        ├── 2020s/
        └── digital/
```

Each gallery uses simple, responsive grids with lazy-loaded images and clean typography.  
The **Professional** page reuses content from `resume.html` and links to LinkedIn and GitHub.

---

## Security & GRC Considerations

- **IAM least privilege** for all roles and service access  
- **S3 encryption** (AES-256 or KMS) and **CloudFront OAC** for secure delivery  
- **DynamoDB encryption-at-rest**  
- **CloudTrail + CloudWatch** enabled for full auditability  
- **CI/CD** enforces version control and deployment integrity  

### Example Control Mapping

| Framework / Control | Implementation Example |
|----------------------|------------------------|
| ISO 27001 A.8 & A.12 | S3 versioning, encrypted storage |
| ISO 27001 A.9 | IAM least-privilege roles |
| NIST CSF DE.CM-7 | CloudTrail + CloudWatch monitoring |


---

## Deployment Process

1. **S3**
   - Create a private S3 bucket for `resume-site`.
   - Enable default encryption and block public access.

2. **CloudFront**
   - Create a distribution with S3 as origin via OAC.
   - Configure default root object: `index.html`.
   - Attach ACM certificate for custom domain (optional but recommended).

3. **Visitor Counter**
   - Create DynamoDB table (e.g., `crc-visitors`) with partition key `id`.
   - Implement Lambda function to:
     - `GET` current count.
     - Increment and return updated count.
   - Deploy API Gateway endpoint and integrate with Lambda.
   - Enable CORS for the CloudFront domain.

4. **CI/CD (GitHub Actions)**
   - On push to `main`:
     - Sync `resume-site/` to S3.
     - Invalidate CloudFront cache.

5. **Monitoring**
   - Enable CloudWatch logs for Lambda and API Gateway.
   - Use CloudTrail for API activity and audit events.

---

## Root Folder Structure

```text
cloud-resume-challenge/
├── README.md                     # Project overview
├── crc-plan.md                   # Planning & implementation notes (this file)
├── diagrams/
│   └── architecture.png
├── infrastructure/               # IaC (CloudFormation/Terraform/SAM/CDK)
│   └── visitor-counter.yml       # Example: visitor counter stack
├── resume-site/                  # Static website source
│   ├── *.html
│   └── assets/
└── docs/
    └── site-implementation.md    # Detailed CRC requirement mapping (planned)
```

---

## Local Testing

```bash
git clone https://github.com/JoelF-GRC/aws-cloud-resume-challenge.git
cd aws-cloud-resume-challenge/resume-site
open index.html
```

When the Lambda + API Gateway are ready, update the `fetch()` URL in `index.html` to point at your API Gateway endpoint for the visitor counter.

---


## Week 1–2 Progress Summary

### Week 1

- Defined project scope and architecture.  
- Created initial diagram (`diagrams/architecture.png`).  
- Set up base repo and folder structure.  
- Drafted CRC plan and security/GRC considerations.  

### Week 2 (In Progress)

- Implement HTML/CSS for gallery + Professional pages.  
- Test locally and adjust layout for mobile responsiveness and dark mode.  
- Prepare Lambda, DynamoDB, and API Gateway for visitor counter.  
- Begin S3 + CloudFront deployment and document CI/CD.  

---

## References

- [Cloud Resume Challenge – AWS](https://cloudresumechallenge.dev/docs/the-challenge/aws/)  
- [AWS Well-Architected Framework](https://aws.amazon.com/architecture/well-architected/)  
- [Amazon S3 Static Website Hosting](https://docs.aws.amazon.com/AmazonS3/latest/dev/WebsiteHosting.html)  
- [AWS Serverless Application Model (SAM)](https://aws.amazon.com/serverless/sam/)

---

## Author

**Joel Flood**  
San Diego, CA  
[LinkedIn](https://www.linkedin.com/in/joelflood/) 
