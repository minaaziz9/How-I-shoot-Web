# 🌍 Reset & Forgot Password Testing

This document details **manual and automated testing** for **password reset vulnerabilities, rate-limiting issues, OTP bypass, and session handling.**

---

## **1️⃣ Identifying Password Reset Pages**

### **Extract Reset & Forgot Password Endpoints**
```bash
cat auth_pages.txt | grep -Ei "/(reset|forgot-password|recover|password-reset)" > reset_pages.txt
```
✅ **Filters password reset-related pages for further testing.**

---

## **2️⃣ Security Checks on Password Reset Pages**

### **Check if HTTPS is Enforced**
- **Ensure reset password links use `https://` instead of `http://`.**
- **Check if reset password requests expose sensitive data in plaintext.**

### **Check if Reset Code Leaks in Response or Email Preview**
- **Inspect HTTP responses to see if reset tokens or OTP codes are leaked.**
- **Check email previews in email clients for sensitive information exposure.**

---

## **3️⃣ Rate-Limiting & OTP Brute-Force Testing**

### **Brute-Force OTP on Reset Page Using `ffuf`**
```bash
ffuf -u https://target.com/reset?otp=FUZZ -w wordlist.txt -mc 200
```
✅ **If OTP codes are brute-forceable, report insufficient rate-limiting.**

---

## **4️⃣ Testing Reset Link Expiration & Replay Attacks**

### **Check if Old Reset Links Remain Valid**
1️⃣ **Request a password reset.**  
2️⃣ **Use the link after a few hours/days.**  
✅ **If the link is still valid, report weak token expiration policy.**

### **Modify Email After Reset Request**
1️⃣ **Request password reset for `victim@gmail.com`.**  
2️⃣ **Change email in account settings before clicking reset link.**  
3️⃣ **Click reset link and check if it still works.**  
✅ **If the reset works after changing emails, report an account takeover issue.**

---

## **5️⃣ Session Handling & Logout Testing**

### **Check if Reset Invalidates Active Sessions**
1️⃣ **Log in to the target account.**  
2️⃣ **Request a password reset & change the password.**  
3️⃣ **Check if old session tokens remain active.**  
✅ **If sessions are not invalidated after password reset, report session mismanagement.**

---

### **🚀 Now, password reset functionalities are fully tested for security vulnerabilities!**

