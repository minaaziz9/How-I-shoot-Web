# 🌍 2FA & OTP Security Testing

This document details **manual and automated testing** for **multi-factor authentication (MFA), OTP brute-force attacks, and bypass techniques.**

---

## **1️⃣ Identifying 2FA & OTP Endpoints**

### **Extract 2FA & OTP Endpoints**
```bash
cat auth_pages.txt | grep -Ei "/(2fa|auth/verify|api/2fa|otp|verify)" > 2fa_pages.txt
```
✅ **Filters pages related to multi-factor authentication for further testing.**

---

## **2️⃣ Testing OTP Weaknesses**

### **Try Logging in Without OTP**
```json
{"email":"me","password":"****","otp":""}
```
✅ **If login succeeds without OTP, report authentication bypass.**

### **Test for Universal OTP Codes**
```bash
Use common OTP values: 000000, 123456, 999999.
```
✅ **If common OTPs work across multiple accounts, report weak OTP generation.**

### **Brute-Force OTP Using `ffuf`**
```bash
ffuf -u https://target.com/2fa?otp=FUZZ -w wordlist.txt -mc 200
```
✅ **If OTP brute-force works, report insufficient rate-limiting.**

---

## **3️⃣ Testing 2FA Bypass Techniques**

### **Check if OTP from Another Account Works**
1️⃣ **Log in to `victim@gmail.com`.**  
2️⃣ **Request OTP but don’t use it.**  
3️⃣ **Use the OTP on another account (`attacker@gmail.com`).**  
✅ **If accepted, report OTP reuse vulnerability.**

### **Disable 2FA via API CSRF Attack**
```json
{"action": "disable_2fa"}
```
✅ **If 2FA can be disabled via API request, report CSRF vulnerability.**

### **Bypass 2FA Using OAuth**
1️⃣ **Check if login via OAuth (Google, Facebook) skips 2FA verification.**  
2️⃣ **If OAuth login doesn’t require OTP, report as a 2FA bypass issue.**

---

### **🚀 Now, 2FA & OTP mechanisms are fully tested for security vulnerabilities!**

