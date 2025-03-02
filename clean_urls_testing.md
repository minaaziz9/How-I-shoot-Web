# 🌍 Clean URLs Testing

This document details **manual and automated testing** on filtered URLs from `clean_urls.txt`, including **authentication, WordPress security, and SSRF testing.**

---

## **1️⃣ Authentication Testing**
Identifying and testing login, signup, reset, and verification endpoints.

### **Extract Authentication Pages**
```bash
cat clean_urls.txt | grep -Ei "/(login|signin|auth|register|signup|reset|forgot|verify|session|password|create-account|recover|password-reset|2fa|otp|verify|xml|upload|data|api/signup|api/login|api/2fa)" > auth_pages.txt
```
✅ **Filters authentication-related pages for further testing.**

#### **Testing Authentication Security**
Refer to:
- **[Register & Signup](register_testing.md)**
- **[Login & Auth](login_testing.md)**
- **[Reset & Forgot Password](reset_testing.md)**
- **[2FA & OTP](2fa_testing.md)**
- **[API & XML Testing](api_xml_testing.md)**

---

## **2️⃣ WordPress Security Testing**
Identifying and analyzing WordPress-based URLs for vulnerabilities.

### **Extract WordPress-Specific URLs**
```bash
cat clean_urls.txt | grep -E "wp-content|wp-admin|wp-includes|xmlrpc.php|wp-login.php|wp-json" > wordpress_urls.txt
```
✅ **Filters WordPress endpoints for security analysis.**

### **Scan WordPress Installations for Vulnerabilities**
```bash
wpscan --url https://target.com --disable-tls-checks --api-token API_KEY -e ap --plugins-detection aggressive
```
✅ **Checks for exposed WordPress users, plugins, and security misconfigurations.**

---

## **3️⃣ SSRF & Open Redirect Testing**
Identifying URLs that may be vulnerable to **Server-Side Request Forgery (SSRF)** and **Open Redirect attacks.**

### **Extract Open Redirect & SSRF Candidates**
```bash
cat clean_urls.txt | grep -Ei "url=|uri=|redirect=|link=|file=|page=|to=|u=|forward=|next=" > ssrfopenredirect_candidates.txt
```
✅ **Finds potential SSRF and open redirect parameters.**

### **Automated SSRF & Open Redirect Testing**
```bash
cat ssrfopenredirect_candidates.txt | xargs -I {} nuclei -t nuclei-templates/http/ssrf.yaml -u "{}"
```
✅ **Runs SSRF-specific `nuclei` templates against extracted candidates.**

---

### **🚀 Now, clean URLs are fully processed and ready for authentication, WordPress, and SSRF testing!**

