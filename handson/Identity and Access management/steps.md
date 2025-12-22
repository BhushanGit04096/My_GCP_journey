# IAM – Hands-on Steps (Console)

---

## Step 1: Open IAM Page

1. Go to **Google Cloud Console**
2. Select your project
3. Navigate to:
   ☰ → **IAM & Admin** → **IAM**

---

## Step 2: View Existing IAM Members

1. Review the list of:
   - Users
   - Service accounts
   - Roles assigned
2. Observe:
   - Owner
   - Editor
   - Viewer roles

📌 This shows who already has access to the project.

---

## Step 3: Assign a Predefined IAM Role to a User

1. Click **Grant Access**
2. Enter a user email
3. Select role:
   - Example: **Viewer**
4. Click **Save**

✅ User now has read-only access to the project.

---

## Step 4: Create a Service Account

1. Go to:
   ☰ → **IAM & Admin** → **Service Accounts**
2. Click **Create Service Account**
3. Enter:
   - Name: `vm-access-sa`
   - ID: auto-generated
4. Click **Create and Continue**

---

## Step 5: Assign Role to Service Account

1. Select a role:
   - Example: **Compute Engine Viewer**
2. Click **Continue**
3. Click **Done**

✅ Service account is created with permissions.

---

## Step 6: Attach Service Account to a VM

1. Go to **Compute Engine → VM instances**
2. Edit an existing VM (or create new)
3. Under **Service Account**:
   - Select `vm-access-sa`
4. Set access scope to **Allow full access to all Cloud APIs**
5. Save changes

📌 This allows the VM to access GCP services securely.

---

## Step 7: Verify Project-Level IAM Binding

1. Go back to **IAM**
2. Confirm:
   - User → assigned role
   - Service account → assigned role
3. Ensure bindings are at **project level**

---

## 🧪 Validation Checklist

✔ User added with predefined role  
✔ Service account created  
✔ Role assigned to service account  
✔ Service account attached to VM  
✔ IAM bindings visible at project level  

---

## ⚠ Common Mistakes

- Assigning **Editor** when **Viewer** is enough
- Using personal credentials instead of service accounts
- Forgetting to attach service account to VM

---

## 🧠 Interview Tip

> “In GCP, IAM follows a who–can–do–what–on–which-resource model.  
> I usually grant predefined roles at the project level and use service accounts for VM and service access.”

