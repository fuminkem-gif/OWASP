
# OWASP ZAP vulnerability scan on DVWA

Target: http://172.17.0.2/dvwa/index.php

Tool: OWASP ZAP 2.13.0

Environment: DVWA running on Locker Docker Network (172.17.0.2)

## 1. Objective

The objective of this exercise was to perform a full web application vulnerability assessment on Damn Vulnerable Web Application (DVWA) using OWASP ZAP, identify potential security flaws, and document both findings and remediation steps.

## 2. Methodology / Workflow

## Step 1: Environment Preparation

. DVWA was deployed and verified running at: `http://172.17.0.2/dvwa/index.php`

. WASP ZAP launched in Standard Mode.

. Browser traffic routed through ZAP using the default local proxy.

## Step 2: Target Setup

. DVWA URL added to the Sites list in ZAP.

. Manual browsing performed to populate site structure and identify entry points.

## Step 3: Spidering (Crawling)

. ZAP Spider executed to crawl hidden directories, parameters, and resources.

. Results validated to ensure full coverage.

## Step 4: Active Scan

. Full Active Scan launched against DVWA.

. ZAP tested for:

i. Injection vulnerabilities

ii. Misconfigurations

iii. Missing or weak security headers

iv. Session and cookie issues

v. Exposure of sensitive information

Step 5: Results Review

. All alerts reviewed in the ZAP Alerts tab.

. Findings analyzed based on severity, confidence level, and ease of exploitation.

## 3. Key Findings

## 3.1 High-Risk Vulnerabilities

. Remote Code Execution: `– CVE-2012-1823`

. Source Code Disclosure: `– CVE-2012-1823`

. Risk Level: High

. Confidence: Medium

. Affected URL: 
```bash
http://172.17.0.2/dvwa/index.php
```

. Impact: Successful exploitation may lead to complete server takeover.

## 3.2 Medium / Low-Risk Vulnerabilities

i. Missing Anti-CSRF Tokens

ii. Content Security Policy (CSP) Header Not Set

iii. Missing Anti-Clickjacking Header (X-Frame-Options)

iv. Cookies Missing HttpOnly Flag

v. Cookies Missing SameSite Attribute

vi. Server Version Disclosure via HTTP Headers

vii. Missing X-Content-Type-Options Header

viii. Authentication Request Exposed

ix. Session Management Weaknesses

x. Discovery of Hidden Files

These weaknesses indicate insufficient hardening and lack of secure configurations.

## 4. Remediation Recommendations

A. Remote Code Execution: `(CVE-2012-1823)`

. Upgrade PHP to a supported secure version.

. Disable PHP CGI if not needed.

. Properly configure:

. allow_url_include

. auto_prepend_file

. Enforce strict input validation and server-side sanitization.

B. Missing Security Headers

. Implement these essential security headers:

i. Content-Security-Policy	Prevent XSS & data injection
ii. X-Frame-Options	Prevent clickjacking
iii. X-Content-Type-Options	Prevent MIME-type sniffing

. Regularly test headers using automated tools (e.g., securityheaders.com).

C. CSRF Protection

. Add CSRF tokens to all sensitive, state-changing requests.

. Validate tokens on the server.

D. Cookie Security

. Set cookies with:

. HttpOnly

. Secure

. SameSite=Strict or Lax

E. General Hardening

. Remove unnecessary files and directories.

. Disable verbose server banners.

. Perform scheduled vulnerability scans and penetration tests.

## 5. Conclusion

The OWASP ZAP vulnerability scan demonstrates how outdated software and insecure configurations can result in critical security risks. ZAP proved effective for uncovering both major exploitation paths and baseline security hygiene issues. Continuous patching, secure configuration, and regular testing remain essential in securing any web application.

6. Disclaimer

This assessment was conducted on DVWA, an intentionally vulnerable application, strictly for educational and ethical hacking practice only.
