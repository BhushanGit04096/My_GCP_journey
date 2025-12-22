
# GCP Hands-on: Create Project & Billing

This section covers the **first and most important step** in Google Cloud Platform (GCP):
creating a project and linking it with a billing account.

Every GCP resource (VMs, storage, databases, networking, IAM, etc.) must belong to a project,
and **billing must be enabled** to use most services.

---

## 🎯 Objectives

- Understand why projects and billing are mandatory in GCP
- Create a new GCP project
- Link the project to an active billing account
- Verify billing status using Cloud Console and CLI

---

## 🧠 Key Concepts

- **Project**: Logical container for all GCP resources
- **Project ID**: Globally unique identifier
- **Billing Account**: Payment profile used to charge usage
- **IAM**: Only users with billing permissions can link accounts

---

## 📂 Files in This Section

- `steps.md` → Step-by-step actions in Cloud Console
- `commands.md` → CLI (gcloud) commands to verify setup

---

## ✅ Prerequisites

- Google account
- GCP free-tier or paid billing account
- Internet access
- Optional: Google Cloud SDK installed

---

## 🧪 Output of This Section

✔ Project created  
✔ Billing account linked  
✔ Ready to create resources (VMs, VPCs, Storage, etc.)

---

📌 **Note**: If billing is not enabled, most GCP services will fail to create resources.
