# 🌍 Web Recon Outline

This document serves as an outline for the **Web Recon Methodology**, with each phase linked to a dedicated file for detailed steps and commands.

---

## **1️⃣ Subdomain Enumeration & Monitoring** → [subdomain_enum.md](subdomain_enum.md)
- **Subdomain Enumeration** (`subfinder`, `assetfinder`, `sublist3r`)
- **Subdomains of Subdomains** (`altdns`)
- **Subdomain Takeover Testing** (`subzy`, `subjack`)
- **Subdomain Monitoring** ([Monitoring Script](https://github.com/minaaziz9/Subdomain-Monitoring-with-Sublist3r-anew-notify))

---

## **2️⃣ HTTPX Analysis & Status Code Testing** → [httpx_analysis.md](httpx_analysis.md)
- **Filtering live hosts** (`httpx`)
- **Testing 300s (Redirects)** → Open Redirects
- **Testing 400s (401, 403)** → Authentication Bypass & 403 Bypass
- **Request Smuggling Testing** (`smuggler`)

---

## **3️⃣ Testing 200 OK Responses** → [live_hosts.md](live_hosts.md)
- **Explore & Test Each Subdomain Individually**
- **Go for URL Extraction** → [url_extraction.md](url_extraction.md)

---

## **4️⃣ URL Gathering & Processing** → [url_extraction.md](url_extraction.md)
- **Extracting URLs** (`gau`, `katana`, `gospider`)
- **Cleaning & Normalization** (`uro`)
- **Extracting JS & PHP files** (`mantra`, `arjun`, `sqlmap`)
- **Sending to Scanners** (`acunetix`, `jaeles`, `nuclei`)

---

## **5️⃣ Clean URLs: Authentication, WordPress & SSRF Testing** → [clean_urls_testing.md](clean_urls_testing.md)
- **Authentication Testing** (Login, Register, Reset, 2FA, OAuth Bypass)
- **WordPress Security Testing** (`wpscan`)
- **SSRF & Open Redirects** (`nuclei`, `burp`)  

---



