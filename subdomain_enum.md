# 🌍 Subdomain Enumeration & Monitoring

This document details the **subdomain enumeration, expansion, takeover testing, and monitoring processes** used in the Web Recon methodology.

---

## **1️⃣ Subdomain Enumeration**
Identifying subdomains using multiple tools to maximize coverage.

### **Commands:**
```bash
subfinder -d target.com -all --recursive -o subs.txt
echo target.com | assetfinder --subs-only >> subs.txt
python3 sublist3r.py -d target.com -o subs.txt
cat subs.txt | anew allsubs.txt
rm subs.txt
```
✅ **Merges results from `subfinder`, `assetfinder`, and `sublist3r` into `allsubs.txt`.**

---

## **2️⃣ Expanding with Subdomains of Subdomains**
Using `altdns` to discover **deeper subdomains** by generating permutations.

### **Command:**
```bash
altdns -i allsubs.txt -o deeper_subs.txt -w wordlist.txt -r -s output.txt
cat deeper_subs.txt | anew allsubs.txt
```
✅ **Expands `allsubs.txt` by including deeper subdomain variations.**

---

## **3️⃣ Subdomain Takeover Testing**
Detecting vulnerable subdomains that might be taken over.

### **Commands:**
```bash
subzy run --targets allsubs.txt --hide_fails --vuln | grep -v -E "Akamai|xyz|available|\-"
subjack -w allsubs.txt -t 50 -o vulnerable_subs.txt -ssl -v
```
✅ **Identifies subdomains pointing to decommissioned services for potential takeover.**

---

## **4️⃣ Subdomain Monitoring**
Continuous tracking of subdomains for changes or new assets.

### **Automated Monitoring Script:**
[🔗 Subdomain-Monitoring-with-Sublist3r-anew-notify](https://github.com/minaaziz9/Subdomain-Monitoring-with-Sublist3r-anew-notify)

✅ **This script periodically checks for new subdomains and alerts you.**

---

### **🚀 With this structured approach, subdomains are comprehensively discovered, monitored, and tested for security risks!**

