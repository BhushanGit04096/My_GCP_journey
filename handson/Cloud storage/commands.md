# GCP Cloud Storage – Hands-on Steps

This document contains step-by-step instructions for performing hands-on operations with Google Cloud Storage.

---

## 1. Create Cloud Storage Buckets

### 1.1 Create a Regional Bucket

1. Go to **Cloud Storage → Buckets**
2. Click **Create**
3. Configure:
   - Bucket name: `my-regional-bucket-<unique-name>`
   - Location type: **Region**
   - Region: `asia-south1`
   - Storage class: Standard
4. Click **Create**

---

### 1.2 Create a Multi-Regional Bucket

1. Click **Create**
2. Configure:
   - Bucket name: `my-multiregional-bucket-<unique-name>`
   - Location type: **Multi-region**
   - Location: `asia`
   - Storage class: Standard
3. Click **Create**

✅ Two buckets created to compare availability and cost models.

---

## 2. Upload and Download Objects

### Upload Objects

1. Open any bucket
2. Click **Upload files**
3. Select a file from your local system

---

### Download Objects

1. Select the uploaded object
2. Click **Download**

✅ Basic object operations verified.

---

## 3. Enable Object Versioning

1. Open the **Regional bucket**
2. Go to **Configuration**
3. Enable **Object Versioning**
4. Save changes

---

### Verify Versioning

1. Upload a file (example: `test.txt`)
2. Modify the file locally
3. Upload again with the same name
4. Open the object and view **Versions**

✅ Multiple versions of the same object retained.

---

## 4. Configure Lifecycle Rules

1. Open the bucket
2. Go to **Lifecycle**
3. Click **Add a rule**
4. Configure:
   - Condition: **Age**
   - Age: `1` day
   - Action: **Delete**
5. Save rule

✅ Objects will be automatically deleted based on lifecycle conditions.

---

## 5. Configure IAM Permissions on Bucket

1. Open the bucket
2. Go to **Permissions**
3. Click **Grant access**
4. Add:
   - Principal: User email or service account
   - Role: **Storage Object Viewer**
5. Save

---

### Verify IAM Access

- User can download objects
- User cannot upload or delete objects

✅ Bucket-level IAM permissions validated.

---

## 6. Generate Signed URLs

1. Open **Cloud Shell**
2. Run the following command:

```bash
gsutil signurl -d 10m ~/.ssh/google_compute_engine.pub gs://my-regional-bucket-<unique-name>/test.txt

