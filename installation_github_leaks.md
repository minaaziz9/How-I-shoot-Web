# 🔧 Installation Guide for GitHub Leaks Tools

This guide provides step-by-step installation instructions for the tools used in the **GitHub Leaks Methodology**.

---

## **1️⃣ Installing `GitDorker`**
```bash
git clone https://github.com/obheda12/GitDorker.git
cd GitDorker
pip3 install -r requirements.txt
```
✅ **Verify Installation:**
```bash
python3 GitDorker.py --help
```

---

## **2️⃣ Installing `git-hound`**
```bash
git clone https://github.com/tillson/git-hound.git
cd git-hound
go build
mv git-hound /usr/local/bin/
```
✅ **Verify Installation:**
```bash
git-hound --help
```

---

## **3️⃣ Installing `truffleHog`**
```bash
git clone https://github.com/trufflesecurity/truffleHog.git
cd truffleHog
pip3 install -r requirements.txt
```
✅ **Verify Installation:**
```bash
python3 trufflehog --help
```

---

## **4️⃣ Installing `PasteHunter`**
```bash
git clone https://github.com/kevthehermit/PasteHunter.git
cd PasteHunter
pip3 install -r requirements.txt
```
✅ **Verify Installation:**
```bash
python3 pastehunter.py --help
```

---

## **5️⃣ Installing `notify` for Real-Time Alerts**
```bash
go install -v github.com/projectdiscovery/notify/cmd/notify@latest
```
✅ **Configure Slack Webhook in `~/.config/notify/provider-config.yaml`**
```yaml
slack:
  - id: "slack-notifications"
    token: "https://hooks.slack.com/services/XXXXX/YYYYY/ZZZZZ"
```
✅ **Test Notification:**
```bash
echo "Test notification" | notify -silent -provider slack-notifications
```

---

## **6️⃣ Setting Up Continuous Monitoring**
Once the tools are installed, run the monitoring script from the [GitHub Leaks Methodology](github_leaks.md):
```bash
chmod +x monitor_github_leaks.sh
nohup ./monitor_github_leaks.sh &
```
✅ This will run the monitoring process **in the background**, checking for leaks every hour and sending alerts via `notify`.

---

✅ **Now all tools are installed and configured for GitHub leak detection!** 🚀

