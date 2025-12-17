# GCP Cloud Storage – Hands-on

This module covers hands-on implementation of **Google Cloud Storage (GCS)**, focusing on bucket creation, object management, access control, and cost optimization features. The goal is to understand how object storage works in real-world GCP environments.

---

## 📌 Topics Covered

- Create Cloud Storage buckets
- Upload and download objects
- IAM permissions on buckets
- Object lifecycle rules
- Object versioning
- Signed URLs for temporary access
- Transfer Jobs (overview)

---

## 🧱 Bucket Types

Two types of buckets were created to understand availability and cost trade-offs:

- **Regional Bucket**
  - Data stored in a single region
  - Lower latency and cost
- **Multi-Regional Bucket**
  - Data replicated across multiple regions
  - Higher availability and durability

---

## 📂 Object Operations

Objects were uploaded and downloaded using both:
- Google Cloud Console
- `gsutil` commands

This validated object access and storage behavior in GCS.

---

## 🔐 IAM Permissions

Bucket-level IAM permissions were applied to control access:

- **Storage Object Viewer** – Read-only access
- **Storage Object Admin** – Full object control

This demonstrates fine-grained access control without granting project-wide permissions.

---

## ♻️ Lifecycle Rules

Lifecycle rules were configured to automatically manage objects based on age:

- Delete objects after a defined number of days

This helps reduce storage costs by automating cleanup.

---

## 🕒 Object Versioning

Object versioning was enabled on the bucket to:

- Preserve older versions of objects
- Recover data from accidental overwrites or deletions

Multiple versions of the same object were verified.

---

## 🔗 Signed URLs

Signed URLs were generated to provide **temporary access** to private objects without modifying IAM policies.

Use cases:
- Secure file sharing
- Time-bound downloads

---

## 🔁 Transfer Jobs (Overview)

Transfer Jobs were explored conceptually to understand:
- Large-scale data migration
- Scheduled transfers
- Data movement between cloud providers or on-prem systems

---

## ✅ Summary

This hands-on demonstrated core Cloud Storage capabilities, including secure access, lifecycle management, and object versioning. These features are critical for building scalable and cost-efficient storage solutions in GCP.

---

## 📸 Screenshots

All relevant screenshots for each step are available in the `screenshots/` directory.
