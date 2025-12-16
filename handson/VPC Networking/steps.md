# GCP VPC Networking – Hands-on Steps

This document contains step-by-step implementation details of my GCP VPC Networking hands-on practice.

---

## 1. Custom VPC Creation

1. Open Google Cloud Console  
2. Go to **VPC network → VPC networks**
3. Click **Create VPC network**
4. Configuration:
   - Name: `custom-vpc`
   - Subnet creation mode: **Custom**
   - MTU: Default
   - Dynamic routing mode: Regional
5. Click **Create**

✅ Result: Custom VPC created without auto-generated subnets.

**Why:**  
Custom VPC provides full control over IP addressing and is preferred in production environments.

---

## 2. Subnet Creation (Custom Mode)

1. Go to **VPC network → VPC networks**
2. Open `custom-vpc`
3. Click **Add subnet**
4. Configuration:
   - Name: `subnet-asia-south1`
   - Region: `asia-south1`
   - IP range: `10.10.0.0/24`
   - Private Google Access: Enabled
5. Click **Add**

✅ Result: Regional subnet created with controlled CIDR range.

**Note:**  
Auto mode creates subnets automatically in all regions, whereas custom mode requires manual subnet creation.

---

## 3. Firewall Rules

### 3.1 Allow SSH Access

1. Go to **VPC network → Firewall**
2. Click **Create firewall rule**
3. Configuration:
   - Name: `allow-ssh`
   - Direction: Ingress
   - Targets: All instances
   - Source IP ranges: `<your-public-ip>/32`
   - Protocols and ports: TCP `22`
4. Click **Create**

---

### 3.2 Allow Application Port (8080)

1. Create another firewall rule
2. Configuration:
   - Name: `allow-8080`
   - Direction: Ingress
   - Source IP ranges: `0.0.0.0/0`
   - Protocols and ports: TCP `8080`
3. Click **Create**

✅ Result: SSH and application traffic allowed as per rules.

**Why:**  
Firewall rules in GCP are applied at the VPC level and are stateful.

---

## 4. Routes

1. Go to **VPC network → Routes**
2. Review default routes:
   - `0.0.0.0/0` → Internet Gateway
   - Subnet-specific routes
3. Observe route priorities

✅ Result: Understood how traffic is routed within and outside the VPC.

**Key Understanding:**  
- Routes decide *where* traffic goes  
- Firewall rules decide *whether* traffic is allowed

---

## 5. VPC Peering

1. Create another VPC: `peer-vpc`
2. Create a subnet with a **non-overlapping CIDR**
3. Go to **VPC network → VPC network peering**
4. Click **Create connection**
5. Configure peering between:
   - `custom-vpc` ↔ `peer-vpc`
6. Accept peering from both sides

7. Launch test VMs in both VPCs
8. Test connectivity using private IPs

✅ Result: Private communication established between VPCs.

**Limitations Observed:**
- No overlapping CIDRs
- No transitive peering

---

## 6. Shared VPC

1. Designated one project as **Host Project**
2. Enabled **Shared VPC** in host project
3. Attached **Service Project**
4. Granted required IAM roles
5. Created VM in service project using host project subnet

✅ Result: VM successfully used shared network resources.

**Why:**  
Shared VPC enables centralized network control across multiple projects.

---

## 7. Cloud NAT

1. Created a VM **without public IP**
2. Verified no internet access
3. Go to **Network services → Cloud NAT**
4. Created NAT configuration:
   - Associated with `custom-vpc`
   - Auto-allocate NAT IPs
5. Retested internet connectivity

✅ Result: VM accessed internet without public IP.

**Use Case:**  
Secure outbound internet access for private instances.

---

## 8. Load Balancers (Introduction)

1. Explored **Load balancing** section in GCP
2. Reviewed types:
   - HTTP(S) Load Balancer (Global)
   - TCP/UDP Load Balancer (Regional)
3. Understood backend services and health checks

✅ Result: Basic understanding of GCP load balancing architecture.

---

## ✅ Summary

This hands-on covered end-to-end VPC networking concepts with real configuration, testing, and validation aligned to production use cases.

