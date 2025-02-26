# 🛠️ Bug Bounty Tools Reference Guide

This document provides a categorized list of tools used for **bug bounty hunting, reconnaissance, exploitation, and automation**.

## **🔍 Recon & Asset Discovery**
| **Tool**         | **Function** |
|------------------|-------------|
| `amass` | ASN lookup, subdomain enumeration |
| `subfinder` | Passive subdomain discovery |
| `assetfinder` | Discover subdomains via search engines |
| `Chaos` | Subdomain enumeration from Bug Bounty DB |
| `altdns` | Subdomain permutation discovery |
| `SecurityTrails` | Online subdomain search |
| `Sublist3r` | Subdomain enumeration tool |
| `shrewdeye.app` | Passive recon |
| `httpx` | Check live subdomains |
| `uncover` | Shodan & Censys asset discovery |
| `shodan` | Find exposed assets & services |
| `censys` | Identify exposed servers & services |

## **📌 Subdomain Takeover**
| **Tool** | **Function** |
|---------|-------------|
| `subzy` | Detect vulnerable subdomains for takeover |
| `subjack` | Check for subdomain hijacking risks |

## **☁️ Cloud Security**
| **Tool** | **Function** |
|---------|-------------|
| `lazys3` | Find misconfigured AWS S3 buckets |
| `cloud_enum` | Discover cloud assets (AWS, GCP, Azure) |
| `GCPBucketBrute` | Google Cloud bucket enumeration |

## **🕵️‍♂️ Web Crawling & URL Enumeration**
| **Tool** | **Function** |
|---------|-------------|
| `katana` | Find URLs in JavaScript files |
| `waybackurls` | Extract historical URLs from the Wayback Machine |
| `gospider` | Web spidering |
| `uro` | Normalize & remove duplicate URLs |
| `gau` | Extract URLs from Google & Archive sources |

## **⚡ WordPress Security**
| **Tool** | **Function** |
|---------|-------------|
| `wpscan` | WordPress vulnerability scanner |
| `nuclei` | Check for WordPress-specific CVEs |
| `httpx` | Identify live WordPress sites |
| `searchsploit` | Find exploits for outdated WordPress versions |

## **🛠️ API & Parameter Discovery**
| **Tool** | **Function** |
|---------|-------------|
| `arjun` | Find hidden GET & POST parameters |
| `LinkFinder` | Extract API endpoints from JavaScript files |
| `Mantra` | Find API keys & secrets in JS files |
| `GitDorker` | Find leaked API keys in GitHub |
| `truffleHog` | Scan GitHub for secrets & credentials |
| `git-hound` | Find sensitive info in GitHub repos |
| `PasteHunter` | Search paste sites for leaked data |

## **🚀 Vulnerability Scanning & Exploitation**
| **Tool** | **Function** |
|---------|-------------|
| `nuclei` | Scan for known vulnerabilities (CVE detection) |
| `jaeles` | Web security automation |
| `sqlmap` | Automated SQL injection exploitation |
| `smuggler` | Detect HTTP request smuggling |
| `403bypasser` | Bypass 403 forbidden pages |
| `Pemburu` | Test authentication bypass on 401 pages |
| `XSS Hunter` | Blind XSS payload testing |

## **🔄 Open Redirect & SSRF Testing**
| **Tool** | **Function** |
|---------|-------------|
| `qsreplace` | Replace parameters in URLs for SSRF/Open Redirect testing |
| `burp collaborator` | Detect external interactions (SSRF) |
| `nuclei` | Use Open Redirect & SSRF detection templates |

## **🔧 Manual Testing & Fuzzing**
| **Tool** | **Function** |
|---------|-------------|
| `ffuf` | Directory brute-forcing |
| `dirsearch` | Find hidden directories & files |
| `Burp Suite` | Manual security testing |
| `Turbo Intruder` | High-speed request manipulation |
| `xsstrike` | Automated XSS fuzzing |
| `dalfox` | Advanced XSS scanning |

## **🔑 JWT & Session Testing**
| **Tool** | **Function** |
|---------|-------------|
| `jwt.io` | Decode JWT tokens |
| `jwtcrack` | Brute-force JWT secrets |

## **🔔 Automation & Monitoring**
| **Tool** | **Function** |
|---------|-------------|
| `notify` | Send Slack/Discord notifications for new subdomains |
| `Shodan Alerts` | Continuous monitoring for new vulnerabilities |

## **🦊 Firefox Extensions for Bug Bounty**
| **Extension** | **Function** |
|---------|-------------|
| `Wappalyzer` | Identify web technologies |
| `FoxyProxy` | Manage proxies easily |
| `Multi-URL Opener` | Open multiple URLs quickly |
| `Translate Extension` | Translate foreign websites |
| `Firefox Containers` | Isolate browsing sessions |


