#  How I Shoot Web

**A structured methodology for web security testing, bug bounty hunting, and cloud security assessments.**

This repository is designed to showcase my **web security methodology** with **step-by-step guides, tools, and scripts** used for reconnaissance, enumeration, and exploitation. Each phase is linked to a dedicated file with in-depth details and automation scripts.
## ** Methodology Overview**

### **1️ GitHub Secrets & PasteHunter** → [GitHub Leaks Guide](github_leaks.md)
- Finding leaked API keys and credentials (`GitDorker`, `truffleHog`, `git-hound`)
- Repository analysis for sensitive data
- Monitoring GitHub commits and paste sites (`PasteHunter`)
- Setting up automation for continuous monitoring

### **2️ Cloud Hacking** → [Cloud Hacking Guide](cloud_hacking.md)
- AWS, GCP, and Azure security testing
- S3/GCP bucket enumeration and exploitation (`lazys3`, `cloud_enum`)
  
### **3️ IP & CIDR (Network & Services)** → [Network Recon Guide](network_recon.md)
- Discovering IP ranges and ASN mapping (`amass`, `shodan`, `censys`, `uncover`)
- Scanning for exposed services (`nmap`, `masscan`)
- Exploiting misconfigured services (SMB, RDP, SSH, etc.)
- Continuous monitoring for new vulnerabilities (`Shodan alerts`)

### **4️ Domains (Web Applications)** → [Web App Hacking Guide](web_recon.md)
- **Processing `domains.txt`** → Enumeration with (`subfinder`, `amass`, `assetfinder`)
- **Subdomain Monitoring** → Automating tracking (`Sublist3r`, `notify`)
- **Live Hosts & URL Extraction** → (`httpx`, `katana`, `gau`, `waybackurls`)
- **JavaScript Analysis & API Discovery** → (`mantra`, `nuclei`, `LinkFinder`)
- **Vulnerability Testing** → (`sqlmap`, `dalfox`, `xsstrike`, `ffuf`, `nuclei`)
- **Authentication & JWT Testing** → (`Burp Suite`, `jwt.io`, `jwtcrack`)
- **Exploiting WordPress, SSRF, Open Redirects** → (`wpscan`, `qsreplace`, `nuclei`)
- **Manual Testing Techniques** → (`xss`, `sqli`, `logic vulnerabilities`)
---

## ** Why This Project?**
🔹 **Real-World Testing Methodology** → Built from hands-on experience in web security testing.
🔹 **Automated & Manual Testing** → Combines automation scripts with deep manual testing techniques.
🔹 **Structured & Expandable** → Each phase links to dedicated sections with in-depth details.

 **Start Exploring:** Click on the phase links above to dive into each topic. More automation scripts and case studies will be added soon!

---

---
 **Maintainer:** Mina Aziz  
 minaaziz@arizona.edu  
 [Portfolio](https://minaaziz9.github.io/Mina-Portfolio) • [GitHub](github.com/minaaziz9)

