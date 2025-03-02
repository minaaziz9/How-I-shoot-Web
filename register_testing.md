# 🌍 Register & Signup Testing

This document details **manual and automated testing** for **registration and signup vulnerabilities**, including **pre-account takeover, XSS, and authentication misconfigurations.**

---

## **1️⃣ Identifying Registration & Signup Pages**

### **Extract Registration & Signup Endpoints**
```bash
cat auth_pages.txt | grep -Ei "/(register|signup|create-account|api/signup)" > register_pages.txt
```
✅ **Filters registration-related pages for further testing.**

---

## **2️⃣ Pre-Account Takeover Testing**

### **Test Registration as an Admin User**
```bash
register with admin@target.com and observe if the account is created.
```
✅ **If successful, report pre-account takeover vulnerability.**

### **Modify Email After Signup Before Verification**
1️⃣ **Sign up with `hacker@gmail.com`.**  
2️⃣ **Receive confirmation email but don’t click.**  
3️⃣ **Change email to `victim@gmail.com` in settings.**  
4️⃣ **Click the old confirmation link.**  
✅ **If `victim@gmail.com` is verified, report email misconfiguration.**  

---

## **3️⃣ 2FA Misconfiguration Testing**

### **Enable 2FA Without Email Verification**
1️⃣ **Sign up with `victim@gmail.com` but do not verify.**  
2️⃣ **Log in to the account and enable 2FA.**  
✅ **If 2FA can be enabled without verifying email, report misconfiguration.**

---

## **4️⃣ Cross-Site Scripting (XSS) Testing**

### **Inject XSS Payloads in Registration Fields**
```html
<svg/onload=confirm()>
">"'><svg onload=alert('XSS')>
<script>alert()</script>
<img src=x onerror=confirm``>
```
✅ **Test these payloads in username, email, and profile fields.**

---

### **🚀 Now, registration & signup pages are fully tested for security vulnerabilities!**

