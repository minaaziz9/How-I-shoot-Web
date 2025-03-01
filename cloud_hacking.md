# ☁️ How I Do Cloud Hacking

This guide covers how I **enumerate, discover, and exploit misconfigured cloud assets**, specifically focusing on AWS, GCP, and Azure. I use `lazys3` and `cloud_enum` to uncover **exposed storage buckets and cloud resources**.

**For tool installation, refer to [INSTALLATION_cloud_hacking.md](installation_cloud_hacking.md).**

---

## **1️⃣ Enumerating AWS S3 Buckets with `lazys3`**
I use `lazys3` to find **misconfigured S3 buckets** belonging to a target.

### **Step 1: Run `lazys3`**
```bash
python3 lazys3.py targetcompany -k YOUR_AWS_KEY -s
```
✅ **What This Does?**
- Searches for **publicly accessible S3 buckets**.
- Identifies misconfigured **ACLs (read/write access).**
- Checks for **exposed files and backups.**

### **Step 2: Check If the Bucket Allows Listing**
```bash
aws s3 ls s3://targetcompany-bucket --no-sign-request
```
✅ If **listing is allowed**, I check for **sensitive files**.

### **Step 3: Try to Download Files**
```bash
aws s3 cp s3://targetcompany-bucket/backup.zip . --no-sign-request
```
✅ If files can be downloaded, **report the misconfiguration!**

---

## **2️⃣ Enumerating AWS, GCP, and Azure with `cloud_enum`**
I use `cloud_enum` to find **cloud assets** across AWS, GCP, and Azure.

### **Step 1: Run `cloud_enum` Against the Target**
```bash
python3 cloud_enum.py -k targetcompany --scan
```
✅ **What This Does?**
- Searches for **S3, GCP, and Azure storage buckets**.
- Finds **Cloudfront/CDN assets**.
- Identifies **public and misconfigured storage resources.**

### **Step 2: Check Bucket Permissions**
Once I identify cloud storage buckets, I test for **misconfigured permissions**.

✅ **For AWS S3 Buckets:**
```bash
aws s3 ls s3://targetcompany-public --no-sign-request
```
✅ **For Azure Blobs:**
```bash
az storage blob list --container-name targetcontainer --account-name targetcompany
```
✅ **For GCP Buckets:**
```bash
gsutil ls -r gs://targetcompany-public
```

### **Step 3: Test for Metadata Exposure (SSRF to Cloud Metadata)**
If a web application is linked to the cloud, I check for **cloud metadata exposure via SSRF.**

```bash
curl http://169.254.169.254/latest/meta-data/
```
✅ If I get a **response from the cloud metadata service**, I attempt privilege escalation.

---

## **🚀 Summary of My Cloud Hacking Approach**
| **Tool** | **Purpose** |
|---------|-------------|
| `lazys3` | Finds AWS S3 buckets and misconfigured permissions |
| `cloud_enum` | Scans AWS, GCP, and Azure for exposed cloud assets |
| `aws cli` | Checks S3 bucket access & downloads files |
| `az cli` | Tests Azure storage permissions |
| `gsutil` | Checks GCP storage access |
| `curl` | Exploits cloud metadata services via SSRF |

✅ **By using `lazys3` and `cloud_enum`, I can efficiently discover misconfigured cloud resources and report security risks!** 🚀

