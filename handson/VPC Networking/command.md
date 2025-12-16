# GCP VPC Networking – Commands (Aligned to Hands-on Steps)

## Set Project, Region, Zone
gcloud config set project <PROJECT_ID>
gcloud config set compute/region asia-south1
gcloud config set compute/zone asia-south1-a

## 1. Custom VPC Creation
gcloud compute networks create custom-vpc \
  --subnet-mode=custom \
  --bgp-routing-mode=regional

## 2. Subnet Creation (Custom Mode)
gcloud compute networks subnets create subnet-asia-south1 \
  --network=custom-vpc \
  --region=asia-south1 \
  --range=10.10.0.0/24 \
  --enable-private-ip-google-access

## 3. Firewall Rules

## 3.1 Allow SSH Access
gcloud compute firewall-rules create allow-ssh \
  --network=custom-vpc \
  --direction=INGRESS \
  --priority=1000 \
  --action=ALLOW \
  --rules=tcp:22 \
  --source-ranges=<YOUR_PUBLIC_IP>/32

## 3.2 Allow Application Port (8080)
gcloud compute firewall-rules create allow-8080 \
  --network=custom-vpc \
  --direction=INGRESS \
  --priority=1000 \
  --action=ALLOW \
  --rules=tcp:8080 \
  --source-ranges=0.0.0.0/0

## 4. Routes – View Default Routes
gcloud compute routes list --filter="network:custom-vpc"

## 5. VPC Peering

## Create Peer VPC
gcloud compute networks create peer-vpc \
  --subnet-mode=custom

## Create Subnet in Peer VPC
gcloud compute networks subnets create peer-subnet \
  --network=peer-vpc \
  --region=asia-south1 \
  --range=10.20.0.0/24

## Create VPC Peering (custom-vpc → peer-vpc)
gcloud compute networks peerings create custom-to-peer \
  --network=custom-vpc \
  --peer-network=peer-vpc

## Create VPC Peering (peer-vpc → custom-vpc)
gcloud compute networks peerings create peer-to-custom \
  --network=peer-vpc \
  --peer-network=custom-vpc

## Test VPC Peering Connectivity
ping <PEER_VM_PRIVATE_IP>

## 6. Shared VPC (High-level Commands)

## Enable Host Project
gcloud compute shared-vpc enable <HOST_PROJECT_ID>

## Attach Service Project
gcloud compute shared-vpc associated-projects add <SERVICE_PROJECT_ID> \
  --host-project=<HOST_PROJECT_ID>

## 7. Cloud NAT

## Create Cloud Router
gcloud compute routers create nat-router \
  --network=custom-vpc \
  --region=asia-south1

## Configure Cloud NAT
gcloud compute routers nats create cloud-nat-config \
  --router=nat-router \
  --router-region=asia-south1 \
  --auto-allocate-nat-external-ips \
  --nat-all-subnet-ip-ranges

## Test Internet Connectivity After NAT
curl https://www.google.com

## 8. Load Balancers (Intro – Listing Types)
gcloud compute forwarding-rules list
