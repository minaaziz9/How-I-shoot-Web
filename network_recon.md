# 🌐 How I Do Network Recon (IP & CIDR)

This guide outlines my **two-pronged approach** to discovering publicly exposed network assets using **ASN enumeration and company name-based reconnaissance**.

**For tool installation, refer to [INSTALLATION_network_recon.md](INSTALLATION_network_recon.md).**

---

## **1️⃣ ASN-Based Reconnaissance**
This method focuses on extracting IP ranges using ASN lookup and scanning them for exposed services.

### **Step 1: Identify ASN for the Target**
I use `amass` to fetch ASN information.
```bash
amass intel -org "Target Company" -o asn_results.txt
```
✅ **What This Does?**
- Finds the **Autonomous System Numbers (ASN)** associated with the target.
- Identifies registered IP ranges that the company owns.

### **Step 2: Extract IP Ranges**
I filter the ASN results for **valid IP ranges**.
```bash
grep -oE "([0-9]{1,3}\.){3}[0-9]{1,3}/[0-9]+" asn_results.txt > ipranges.txt
```
✅ **Now I have a list of IP ranges to scan.**

### **Step 3: Find Publicly Exposed Assets**
I run `uncover` to identify publicly accessible servers within the IP ranges.
```bash
uncover -i ipranges.txt -o uncover_asn_results.txt
```
✅ This finds **open services, web apps, and accessible network assets**.

### **Step 4: Scan for Known CVEs with `Nuclei`**
After identifying live hosts, I use `nuclei` to check for vulnerabilities.
```bash
cat uncover_asn_results.txt | nuclei -t cves/ -o cve_results.txt
```
✅ This checks for **exploitable vulnerabilities** in the exposed services.

### **Step 5: Perform Shodan Searches on Found Assets**
Once I have the IPs, I use `shodan` to get **detailed intelligence on open ports and known exploits**.
```bash
shodan search "net:`cat ipranges.txt`"
```
✅ This provides **deep insights into running services and risks.**

---

## **2️⃣ Company Name-Based Reconnaissance**
Instead of using ASN, I search for **public assets tied to the company name.**

### **Step 1: Use `uncover` with the Company Name**
```bash
uncover -q 'org:"Target Company"' -e shodan,censys -o uncovered_assets.txt
```
✅ This identifies **all publicly listed IPs and domains** related to the company.

### **Step 2: Set Up Continuous Shodan Monitoring**
I configure **Shodan Alerts** to notify me of new exposures.
```bash
shodan alert create --trigger "new_vuln" "org:Target Company"
```
✅ This keeps me updated on **newly exposed services** over time.

---

## **🚀 Summary of My Network Recon Approach**
| **Method** | **Tools Used** | **Outcome** |
|-----------|--------------|------------|
| **ASN-Based Recon** | `amass`, `grep`, `uncover`, `nuclei`, `shodan` | Find exposed assets via ASN & scan for CVEs |
| **Company Name-Based Recon** | `uncover`, `shodan alerts` | Discover assets linked to company name & monitor changes |

✅ **By combining ASN-based recon with company name searches, I can find and monitor exposed network assets effectively!** 🚀

