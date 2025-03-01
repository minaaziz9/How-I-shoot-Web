# 🔧 Installation Guide for Cloud Hacking Tools

This guide explains how I install and configure the tools I use for **cloud security assessments**, including `lazys3` and `cloud_enum`.

---

## **1️⃣ Installing `lazys3`**
I use `lazys3` to find **publicly accessible AWS S3 buckets**.
```bash
git clone https://github.com/nahamsec/lazys3.git
cd lazys3
pip3 install -r requirements.txt
```
✅ **To verify installation, I run:**
```bash
python3 lazys3.py --help
```

---

## **2️⃣ Installing `cloud_enum`**
I use `cloud_enum` to enumerate **AWS, GCP, and Azure storage buckets**.
```bash
git clone https://github.com/initstring/cloud_enum.git
cd cloud_enum
pip3 install -r requirements.txt
```
✅ **To verify installation, I run:**
```bash
python3 cloud_enum.py --help
```

---

## **3️⃣ Installing Cloud CLI Tools**
These are necessary for checking permissions and downloading exposed files.

✅ **AWS CLI (For AWS S3 bucket testing)**
```bash
sudo apt install awscli -y
aws configure  # Set up credentials if needed
```

✅ **Azure CLI (For Azure Blob storage testing)**
```bash
curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash
az login  # Authenticate to Azure
```

✅ **Google Cloud SDK (For GCP storage testing)**
```bash
curl https://sdk.cloud.google.com | bash
exec -l $SHELL
gcloud auth login  # Authenticate to Google Cloud
```

---

✅ **Now all tools are installed and configured for cloud hacking!** 🚀

