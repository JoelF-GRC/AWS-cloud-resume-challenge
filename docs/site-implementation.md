# Site Implementation Document

_For joelflood.com — Art Portfolio + Professional Resume Site_

## 1. Objective

The objective of this project is to design and deploy a modern, minimal, highly secure, cost-efficient, static website hosted entirely on AWS.  
The site features:

- A visual-first **art portfolio** (primary focus)
    
- A clean, accessible **professional resume page**
  
- Leverage AWS services to demonstrate working knowledge of AWS ecosystem
    
- Links to **GitHub projects**, including Cloud Resume Challenge and GRC/AWS repos
    
- Optional pages for bicycles, Daniel Rebour drawings, and new artwork categories
    
The implementation follows AWS Cloud Resume Challenge principles while expanding the scope into a full personal portfolio.

---

## 2. Architecture Overview

### 2.1 High-Level Diagram

**Frontend static hosting:**

- Amazon S3 (private bucket with OAI)
    
- Amazon CloudFront (global CDN)
    
- Route 53 (DNS + apex domain)
    
- ACM (TLS certificates)
    

**Backend / dynamic features (optional or future):**

- Lambda + API Gateway for visitor counter
    
- DynamoDB visitor table
    
- CloudWatch logs for request tracking
    

**Security:**

- CloudFront WAF (optional)
    
- Geo-restriction (non-US allowed list)
    
- Strict CSP + security headers
    
- DNSSEC on Route 53
    
---

## 3. Implementation Components

### 3.1 S3 Bucket Setup

- **Bucket name:** `joelflood.com` (public access BLOCKED)
    
- **Website hosting disabled** (CloudFront handles routing)
    
- **OAC (Origin Access Control)** configured so only CloudFront can access the S3 bucket via SigV4-signed requests, keeping the bucket fully private
    
- **Clean URLs (no .html)** implemented through CloudFront’s behavior and default root object
    
### 3.2 CloudFront Distribution

- Default behavior → S3 bucket origin
    
- Custom error pages for 403 → redirect to `/index.html`
    
- Geo-blocking enabled to only allow limited whitelisted countries
        
- HTTP → HTTPS enforced
    
- Long TTL caching enabled for images, short TTL for HTML
    
### 3.3 TLS Certificates

- ACM certificate issued for:
    
    - `joelflood.com`
        
    - `www.joelflood.com`
        
- Attached to CloudFront
    
### 3.4 Route 53

- Hosted zone for domain
    
- A and AAAA records pointing to CloudFront
    
- CNAME for `www` to CloudFront
    
- DNSSEC enabled on the zone
    
- Nameservers updated at the registrar
    
---

## 4. Frontend Implementation

### 4.1 File & Folder Structure

|── resume-site/              # Static website
│   ├── robots.txt			  # Block "/images/" from search engines	
│   ├── sitemap.xml
│   ├── about.html
│   ├── 1990s.html
│   ├── 2000s.html
│   ├── 2010s.html
│   ├── 2020s.html
│   ├── digital-media.html
│   ├── professional.html	  # Resume
│   ├── favicon-16.png
│   ├── favicon-32.png
│   ├── favicon.ico
│   └── assets/
│       ├── css/style.css
│       └── images/           # Art images
│       └── js/main.js

### 4.2 Visual/UX Design

- Minimal, contemporary, **not 2010-style**
    
- Typography: Google Fonts **Inter** (modern, accessible)
    
- Consistent spacing + white space
    
- Art images displayed in grid → tap to open **custom Lightbox**
    
- Light/dark mode harmony (fixes applied)
    
- Fully responsive:
    
    - Mobile-first gallery
        
    - Hamburger nav with JS
        
    - Grid auto-fit for artwork
        
### 4.3 Resume Page

Resume page is located at `/professional` on your live site. Current uploaded version referenced here:  

Improvements added:

- Certificate chips
    
- Clean typography
    
- Header with certifications inline
    
- Accessible section labels (`aria-labelledby`)
    
- Visitor counter integration at bottom
    
### 4.4 Lightbox Implementation

- CSS + JS solution avoids external libraries
    
- JS listens for `click` events on `.gallery-item`
    
- Closes on backdrop click or `ESC`
    
### 4.5 Navigation

- Global nav included in header
    
- Hamburger menu for mobile only
    
- Uses accessible aria roles
    
- Smooth-scroll for internal anchors
    
---

## 5. Security Hardening

### 5.1 Security Headers

Configured at CloudFront:

- `Strict-Transport-Security: max-age=63072000; includeSubdomains; preload`
    
- `Content-Security-Policy`  
    (carefully refined after initial breakage)
    
- `X-Content-Type-Options: nosniff`
    
- `Referrer-Policy: strict-origin-when-cross-origin`
    
- `Permissions-Policy: camera=(), microphone=(), geolocation=()`
    
- `X-Frame-Options: DENY`

- `Geo-location blocking: set restrictive whitelist of approved countries`
    
Documented issues during implementation:

- CSP initially broke lightbox → fixed by adding `img-src 'self' data:`
    
- Inline JS blocked → converted to external `/main.js`
    
- securityheaders.com scan blocked due to geo-restriction → required allowing Ireland
    
### 5.2 WAF (optional)

Rules you planned to use:

- AWS Managed “Common” rules
    
- Bot Control light
    
- Rate-based throttle (1000 requests / 5 min)
    
- Country allow list
    
### 5.3 Additional Security

- DNSSEC
    
- No public S3 bucket
    
- CloudFront prevents origin exposure
    
- CloudTrail logs bucket/object access
    
---

## 6. Visitor Counter Implementation (Cloud Resume Challenge Requirement)

### 6.1 Architecture

- DynamoDB table:
    
    - pk: `site_visitors`
        
    - counter: number
        
- Lambda function increments + returns visitor count
    
- API Gateway exposes HTTPS endpoint
    
- CORS restricted to `joelflood.com`
    
- JS fetches count on page load
    
### 6.2 Frontend Integration

In `main.js`:

``fetch('https://api.joelflood.com/visitors')   .then(res => res.json())   .then(data => {     document.getElementById('visitor-counter').textContent =       `Visitors: ${data.count}`;   });``

Element on page:

`<div id="visitor-counter" class="visitor-counter" aria-live="polite">   Visitors: … </div>`

---

## 7. Future Enhancements

### 7.1 Terraform Rebuild

A parallel clean implementation entirely in Terraform:

- S3, CloudFront, Route 53, ACM
    
- Lambda/API Gateway
    
- IAM roles
    
- Automated deployments from GitHub Actions
    
### 7.2 CI/CD

Move off AWS GUI:

- GitHub Actions pipeline:
    
    - Validate HTML/CSS
        
    - Upload to S3
        
    - Invalidate CloudFront cache
        
    - Run Lighthouse tests
        
### 7.3 Additional Pages

- `/bicycle` historian archive
    
- `/bicycle/rebour` with:
    
    - Original drawing
        
    - Le Cycle reference
        
    - French text
        
    - English translation
        
### 7.4 Art Metadata

Optional JSON metadata:

- Title
    
- Medium
    
- Year
    
- Tags
    

Used to auto-generate gallery pages.

---

## 8. Maintenance & Operations

### 8.1 Costs

- S3: ~$0.20/month
    
- CloudFront: ~$1–3/month depending on image traffic
    
- Route 53: $0.50/zone, $12/year domain
    
- Lambda/DynamoDB: < $0.10/month
    
### 8.2 Backup Strategy

- GitHub version control handles content
    
- S3 versioning optional for rollback
    
- CloudFront invalidations automated via CI/CD
    
### 8.3 Monitoring

- CloudWatch logs for API
    
- Route 53 health checks optional
    
- AWS Billing alarms
    

---

## 9. Appendix

### 9.1 Referenced Resume Page

The uploaded `professional.html` file incorporated into the project:  

---