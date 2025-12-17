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

1. Click **Create** again
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

1. Upload a file (e.g., `test.txt`)
2. Modify the file locally
3. Upload again with the same name
4. Open the object → view **Versions**

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

### Verify Access

- User can download objects
- User cannot upload or delete objects

✅ Bucket-level IAM permissions validated.

---

## 6. Generate Signed URLs
A Signed URL is a temporary, secure link that lets someone access a private object in Cloud Storage without giving them IAM permissions.
1. Open **Cloud Shell**
2. Run the following command:

"bash
gsutil signurl -d 10m ~/.ssh/google_compute_engine.pub gs://my-regional-bucket/test.txt"

## 7. Transfer Jobs (Hands-on)

### Objective
Create a transfer job to copy objects from one Cloud Storage bucket to another.

---

### Step 7.1: Open Transfer Jobs

1. Go to **Cloud Storage → Transfer**
2. Click **Create a transfer job**

---

### Step 7.2: Configure Source

1. Select **Cloud Storage** as the source
2. Choose:
   - Source bucket: `my-regional-bucket-<unique-name>`
3. Click **Continue**

---

### Step 7.3: Configure Destination

1. Select destination:
   - Destination bucket: `my-multiregional-bucket-<unique-name>`
2. Click **Continue**

---

### Step 7.4: Configure Transfer Settings

1. Configure transfer options:
   - Overwrite objects if different: Optional
   - Delete objects from source after transfer: ❌ Disabled
2. Click **Continue**

---

### Step 7.5: Schedule Transfer

1. Select **Run once**
2. Choose **Run now**
3. Click **Create**

---

### Step 7.6: Verify Transfer

1. Open the created transfer job
2. Verify the job status is **Completed**
3. Confirm objects are available in the destination bucket
