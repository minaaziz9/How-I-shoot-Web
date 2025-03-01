# 🔍 GitHub Leaks Methodology

This guide details the step-by-step process for discovering **leaked API keys, secrets, and credentials** in GitHub repositories using `GitDorker`, `git-hound`, `truffleHog`, and `PasteHunter`.

For tool installation, refer to [INSTALLATION_github_leaks.md](installation_github_leaks.md).

This methodology also includes **continuous monitoring**, ensuring that newly leaked credentials are automatically detected and alerts are sent in real-time.

---

## **1️⃣ GitHub Dorking with `GitDorker`**
### **Step 1: Search for Leaked Secrets**
```bash
python3 GitDorker.py -tf tokens.txt -q "org:TargetCompany" -d dorks.txt -o github_results.txt
```
✅ **What This Does?**
- Uses a **GitHub API token** (`tokens.txt`).
- Searches for **API keys, credentials, and secrets** using `dorks.txt`.
- Stores results in `github_results.txt`.

### **Example Dorks (`dorks.txt`)**
```
org:TargetCompany "aws_access_key"
org:TargetCompany "private_key"
org:TargetCompany "password"
org:TargetCompany "API_KEY"
```

---

## **2️⃣ Searching for Secrets in Repos with `git-hound`**
### **Step 1: Run Git-Hound for Sensitive Information**
```bash
git-hound --config config.yml --subdomain-file targets.txt --output results.txt
```
✅ **What This Does?**
- **Scans repositories for sensitive data**.
- **Extracts subdomains linked to the target**.
- **Finds API keys, credentials, and secrets**.

---

## **3️⃣ Finding Credentials in Git Repos with `truffleHog`**
### **Step 1: Scan a Repository for Secrets**
```bash
trufflehog --regex --entropy=True https://github.com/TargetCompany/repository.git
```
✅ **What This Does?**
- Searches **entire commit history** for leaked credentials.
- Detects **high-entropy secrets like AWS keys and passwords**.

---

## **4️⃣ Finding Leaked Credentials in Paste Sites with `PasteHunter`**
### **Step 1: Search for Leaks in Paste Sites**
```bash
python3 pastehunter.py -s "TargetCompany" -o paste_results.txt
```
✅ **What This Does?**
- **Monitors Pastebin, Ghostbin, and other paste sites**.
- **Finds leaked credentials and sensitive data**.
- **Stores findings in `paste_results.txt`**.

---

## **5️⃣ Continuous Monitoring for GitHub Leaks**
To ensure real-time detection of leaks, set up **automated monitoring** for GitHub and paste sites.

### **Unified Monitoring Script**
Create a script `monitor_github_leaks.sh` that runs all monitoring tools in the background:
```bash
#!/bin/bash
while true; do 
    echo "Running GitHub Dorking..."
    python3 GitDorker.py -tf tokens.txt -q "org:TargetCompany" -d dorks.txt -o github_results.txt;
    
    echo "Running Git-Hound..."
    git-hound --config config.yml --subdomain-file targets.txt --output results.txt;
    
    echo "Running TruffleHog..."
    trufflehog --regex --entropy=True https://github.com/TargetCompany/repository.git;
    
    echo "Running PasteHunter..."
    python3 pastehunter.py -s "TargetCompany" -o paste_results.txt;
    
    echo "Sending notifications if new leaks are found..."
    echo "New GitHub leak detected! Check results." | notify -silent -provider slack-notifications;
    
    sleep 3600; 
done
```
✅ **What This Does?**
- **Runs all four tools every hour** for continuous monitoring.
- **Sends alerts via `notify` if leaks are found.**

### **Make the Script Executable and Run It in the Background**
```bash
chmod +x monitor_github_leaks.sh
nohup ./monitor_github_leaks.sh &
```
✅ This will run the monitoring script **in the background** continuously.

---

## **🚀 Summary of GitHub Leaks Testing**
| **Tool** | **Purpose** |
|---------|-------------|
| `GitDorker` | Finds secrets using GitHub dorking queries |
| `git-hound` | Searches repositories for leaked credentials |
| `truffleHog` | Finds exposed secrets in repository history |
| `PasteHunter` | Identifies leaked credentials in paste sites |
| `notify` | Sends real-time alerts when leaks are detected |

✅ **I use these tools together** for maximum **GitHub recon efficiency**.

