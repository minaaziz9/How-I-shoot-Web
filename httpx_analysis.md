# 🌍 HTTPX Analysis & Status Code Testing

This document details the **live host filtering, status code categorization, and vulnerability testing process** using `httpx`.

---

## **1️⃣ Identifying Live Hosts**
Filtering active subdomains from `allsubs.txt`.

### **Command:**
```bash
cat allsubs.txt | httpx -o httpx_live.txt
```
✅ **Extracts only reachable subdomains and stores them in `httpx_live.txt`.**

---

## **2️⃣ Categorizing HTTP Responses**
We categorize live hosts based on HTTP status codes for targeted testing.

### **Redirects (301/302) – Open Redirect Testing**
```bash
cat httpx_live.txt | httpx -mc 301,302 -o httpx_301_302.txt
```
✅ **Identifies redirects that could be vulnerable to open redirect attacks.**

### **Unauthorized (401) – Authentication Bypass Testing**
```bash
cat httpx_live.txt | httpx -mc 401 -o httpx_401.txt
pemburu -i httpx_401.txt -o pemburu_results.txt
```
✅ **Attempts authentication bypass on unauthorized endpoints.**

### **Forbidden (403) – Access Bypass Testing**
```bash
cat httpx_live.txt | httpx -mc 403 -o httpx_403.txt
403bypasser -u httpx_403.txt -w wordlist.txt
```
✅ **Tests for 403 bypass techniques to access restricted pages.**

### **Request Smuggling Detection**
```bash
cat httpx_live.txt | smuggler.py | tee -a smuggler.txt
```
✅ **Detects potential HTTP request smuggling vulnerabilities.**

---

## **3️⃣ Identifying Live Web Applications (200 OK)**
Filtering `200 OK` responses to find actively running services.

### **Command:**
```bash
cat httpx_live.txt | httpx -mc 200 -o httpx_200.txt
```
✅ **Extracts fully accessible domains for deeper analysis.**

---


