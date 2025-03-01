# 🔧 Installation Guide for Network Recon Tools

This guide explains how I install and configure the tools I use for **network reconnaissance**, including `amass`, `uncover`, `nuclei`, and `shodan`.

---

## **1️⃣ Installing `amass`**
I use `amass` for **ASN lookup and IP range discovery**.
```bash
sudo apt install amass -y
```
✅ **To verify installation, I run:**
```bash
amass --help
```

---

## **2️⃣ Installing `uncover`**
I use `uncover` to find **publicly exposed assets on Shodan, Censys, and other sources**.
```bash
go install -v github.com/projectdiscovery/uncover/cmd/uncover@latest
```
✅ **To verify installation, I run:**
```bash
uncover --help
```

---

## **3️⃣ Installing `nuclei`**
I use `nuclei` to scan for **known CVEs on discovered assets**.
```bash
go install -v github.com/projectdiscovery/nuclei/v2/cmd/nuclei@latest
```
✅ **To verify installation, I run:**
```bash
nuclei --help
```

---

## **4️⃣ Installing `shodan` CLI**
I use `shodan` to gather **detailed intelligence on discovered assets**.
```bash
pip3 install shodan
```
✅ **To verify installation, I run:**
```bash
shodan init YOUR_SHODAN_API_KEY
shodan stats apache
```

---

## **5️⃣ Setting Up Continuous Shodan Monitoring**
I configure **Shodan Alerts** to notify me when new vulnerabilities appear for the target.
```bash
shodan alert create --trigger "new_vuln" "org:Target Company"
```
✅ This will **continuously track newly exposed services** related to the company.

---

✅ **Now all tools are installed and configured for network reconnaissance!** 🚀

