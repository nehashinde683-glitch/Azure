# 🌐 Azure–AWS Site-to-Site VPN Lab  
This lab demonstrates how to build a **Site-to-Site VPN** between **Azure VNet** and **AWS VPC**, enabling secure private communication between virtual machines in both clouds.

---

# 🎯 **Lab Goal**

The goal of this lab is to:

- Create a Virtual Network (VNet) in Azure  
- Create a VM inside Azure VNet  
- Build Azure Virtual Network Gateway  
- Build AWS VPC components (VGW, CGW, VPN Connection, Route Tables)  
- Establish bidirectional Site-to-Site VPN connectivity  
- Verify communication using ping  
- Practice hybrid cloud networking fundamentals  

This is a **complete real-world architecture** used by companies for hybrid connectivity between Azure and AWS.

---

---

# 🟦 **STEP 1 — Create Azure VNet and Subnets**

## 1️⃣ Open Virtual Network
1. Click **Virtual Network**  
   ![](https://github.com/user-attachments/assets/2dcf4737-eeef-4f7b-a937-384088b47e7c)

2. Click **Create**  
   ![](https://github.com/user-attachments/assets/0bc6c4c7-6125-4c83-ac9e-ef2ed43b3b12)

---

## 2️⃣ Enter VNet Details
- Resource Group: **PRATHAM**  
- VNet Name: **V-NET**  
- Region: **Central India**

3. Click **IP Addresses**  
   ![](https://github.com/user-attachments/assets/df530974-4075-4218-93af-283e90dd3c5c)

---

# 🔹 Create Subnet 1 (VM Subnet)

4. Click **Add Subnet**  
5. Subnet Purpose: **Default**  
6. Name: **VM-SUB**  
7. Starting Address: `10.0.1.0`  
8. Subnet Size: `/24`  
9. Click **Add**  

   ![](https://github.com/user-attachments/assets/31cfd727-1b38-4d56-98e5-e3b9ff1b0543)

---

# 🔹 Create Subnet 2 (Gateway Subnet)

10. Click **Add Subnet**  
11. Subnet Purpose: **Virtual Network Gateway**  
12. Name: **GatewaySubnet**  
13. Starting Address: `10.0.2.0`  
14. Size: `/24`  
15. Click **Add**  

16. Click **Review + Create**  
   ![](https://github.com/user-attachments/assets/b36a5f7e-ca74-45f9-adaa-4984f55a1706)

17. Click **Create**  
   ![](https://github.com/user-attachments/assets/30f46b6f-9967-4384-b3c9-ac4aebb18bc6)

---

# 🟩 STEP 2 — Create Azure VM

## 1️⃣ Open Virtual Machines
1. Click **Virtual Machines**  
   ![](https://github.com/user-attachments/assets/fd0a190b-138d-4b66-b1e4-c92879221440)

2. Click **Create → Virtual Machine**  
   ![](https://github.com/user-attachments/assets/1f4b89f9-d058-4b02-87a4-edf2ffba454b)

---

## 2️⃣ Enter VM Details
- Resource Group: **PRATHAM**
- VM Name: **VM-1**
- Region: **Central India**
- Availability Zone: **1**
- Image: **Windows Server**
- Size: **Standard_D2as_v5 (2 vCPUs, 8 GB RAM)**

![](https://github.com/user-attachments/assets/c36586f6-ff1e-4e6c-ac15-ac091d5b93a9)

---

## 3️⃣ Administrator Account
- Username: **VM-1**
- Password: `*******`
- Inbound Port: **RDP (3389)**

![](https://github.com/user-attachments/assets/e3c34404-e6de-49ad-a725-20a906edb901)

---

## 4️⃣ Networking Settings
- Virtual Network: **V-NET**
- Subnet: **VM-SUB**

![](https://github.com/user-attachments/assets/c49423b6-b6a5-49d9-b200-159d82dec072)

Click **Review + Create → Create**  
![](https://github.com/user-attachments/assets/b489d514-50db-4ae7-bf6e-0d84c035689c)

---

# 🛡 STEP 2A — Add NSG Inbound Rule (HTTP Example)

1. Go to **VM → Networking**  
   ![](https://github.com/user-attachments/assets/c0837a10-d834-470f-a3d8-48e9d609b70c)

2. Click **Create port rule**  
3. Select **Inbound port rule**  
   ![](https://github.com/user-attachments/assets/b5948280-c155-40cc-b231-6f15ef8304bf)

### Add Rule:
| Field | Value |
|-------|-------|
| Source | Any |
| Source Port | * |
| Destination | Any |
| Service | HTTP |
| Destination Port | 80 |
| Protocol | TCP |
| Priority | 20 |
| Name | HTTP |

![](https://github.com/user-attachments/assets/6b075b29-4e32-4f5c-99ff-0d41f5cf648a)

---

# 🟦 STEP 2B — Connect to Azure VM (via RDP)

1. Go to VM → **Overview**  
2. Copy the **Public IP**  
   ![](https://github.com/user-attachments/assets/e96883d2-6192-4d4c-87c7-62eecdd8a007)

3. On your computer → search **Remote Desktop Connection**  
   ![](https://github.com/user-attachments/assets/54901e48-daf7-440f-8a69-a8d2b2465720)

4. Enter Public IP  
   ![](https://github.com/user-attachments/assets/8a4d9413-7ab5-4902-941a-1dac9d5be47c)

5. Login with:
- Username: **VM-1**
- Password: `******`

6. Click **Yes**  
   ![](https://github.com/user-attachments/assets/372c55d1-95da-408a-b8cd-31f58a69d931)

---

# 🔥 STEP 2C — Turn OFF Windows Firewall (Required for VPN PING Test)

⚠ **This step is ONLY for LAB / Testing.  
Do NOT turn off firewall in production.**

1. Press **Windows + R**  
2. Type: `firewall.cpl`  
3. Click OK  
   ![](https://github.com/user-attachments/assets/f98bb8dd-2dd7-4686-aefe-cb3b1dbb2bf1)

4. Click **Turn Windows Defender Firewall on or off**  
   ![](https://github.com/user-attachments/assets/6366a21c-025e-4719-a0f5-15d854307148)

5. Turn OFF:
- Private network firewall  
- Public network firewall  

6. Click OK  
   ![](https://github.com/user-attachments/assets/2ebbb8f5-1d7e-4cb1-ad73-e496b5d38cfb)

---

# 🟦 STEP 3 — Create Azure Virtual Network Gateway (VNG)

## 1️⃣ Open Virtual Network Gateway service
1. Click on **Search**
2. Type **vng**
3. Select **Virtual Network Gateway**
   ![](https://github.com/user-attachments/assets/7a699b9b-ea5c-4fad-adc2-106169e80b1b)

---

## 2️⃣ Create New Virtual Network Gateway
1. Click **Create**
   ![](https://github.com/user-attachments/assets/40c8bde5-c645-46f6-9430-e9a7d0a618c9)

---

## 3️⃣ Enter Basic Details
| Field | Value |
|-------|--------|
| Resource Group | PRATHAM |
| Name | VNG |
| Region | Central India |
| Gateway Type | VPN |
| VPN Type | Route-based |
| SKU | VpnGw1 (recommended) |
| Virtual Network | V-NET |
| Subnet | GatewaySubnet |
| Public IP | Create new → VNG-PUB-IP |

![](https://github.com/user-attachments/assets/c4729370-e52a-4408-ac11-91e16248fbe8)

---

## 4️⃣ Disable Unnecessary Options
| Option | Value |
|--------|--------|
| Active-Active Mode | Disabled |
| BGP | Disabled |

![](https://github.com/user-attachments/assets/903ed485-a74a-4aea-8efa-2791910e5807)

---

## 5️⃣ Review and Create
1. Click **Review + Create**
2. Click **Create**

⏳ *Note: VNG creation takes ~20-30 minutes.*

---

# 🟧 PART 4 — AWS VPC CONFIGURATION  
In this step, we will configure AWS networking components required for VPN connectivity with Azure.

---

# 🟠 STEP 4.1 — Create Virtual Private Gateway (VGW)

## 1️⃣ Open AWS Console → Search "VPC"
![](https://github.com/user-attachments/assets/6fd5be68-4138-4ffa-bbc4-a484da2df406)

---

## 2️⃣ Go to "Virtual Private Gateways"
1. Click **Virtual Private Gateways**
2. Click **Create Virtual Private Gateway**
   ![](https://github.com/user-attachments/assets/514265da-29cf-4097-a4d8-4a2738deb3b3)

---

## 3️⃣ Enter Details
| Field | Value |
|-------|--------|
| Name | VPG |
| ASN | Default |

4. Click **Create Virtual Private Gateway**  
   ![](https://github.com/user-attachments/assets/2255cd86-7953-4125-a262-52c6eef13617)

---

## 4️⃣ Attach VGW to VPC
1. Select **VPG**  
2. Click **Actions → Attach to VPC**
   ![](https://github.com/user-attachments/assets/5b15fd7c-3750-49d3-a686-5573daec68b8)

3. Choose **Default VPC**  
4. Click **Attach**
   ![](https://github.com/user-attachments/assets/5738b384-7ece-4ed4-8fd9-ecc379556dc5)

---

# 🟠 STEP 4.2 — Create Customer Gateway (CGW)

1. Click **Customer Gateway**
2. Click **Create Customer Gateway**
   ![](https://github.com/user-attachments/assets/83482745-13dd-4d46-84d9-26cc4901f3de)

---

## Enter Details:
| Field | Value |
|-------|--------|
| Name | AZURE-CGW-TO-AWS |
| IP Address | `4.224.72.113` *(Azure VNG Public IP)* |
| Routing | Static |

Click **Create Customer Gateway**  
![](https://github.com/user-attachments/assets/8965b5ba-393f-4cc5-80b3-ffb62f50693a)

---

# 🟠 STEP 4.3 — Create Site-to-Site VPN Connection

1. Open **Site-to-Site VPN Connections**
2. Click **Create VPN Connection**
   ![](https://github.com/user-attachments/assets/aeec08c5-f3d0-411a-a766-6704e74c842c)

---

## Enter Details:
| Field | Value |
|-------|--------|
| Name | VPN |
| Virtual Private Gateway | VPG |
| Customer Gateway | AZURE-CGW-TO-AWS |
| Routing | Static |
| Static Prefix | `10.0.0.0/16` (Azure VNet CIDR) |

Click **Create VPN Connection**  
![](https://github.com/user-attachments/assets/010f4599-d40a-4370-ab8e-4f87bd5620a3)

![](https://github.com/user-attachments/assets/fa658c61-84db-47d3-8f64-c4712a0a7d49)

---

# 🟠 STEP 4.4 — Update AWS Route Table

1. Open **Route Tables**
2. Select default Route Table
3. Click **Edit Routes**
   ![](https://github.com/user-attachments/assets/ce4b217e-39eb-4222-893b-cd9dad2298d3)

---

## Add Route:
| Destination | Target |
|-------------|--------|
| 10.0.0.0/16 | Virtual Private Gateway |

Click **Save Changes**  
![](https://github.com/user-attachments/assets/4eb728c2-d44f-44fe-83ce-db588544e15b)

---

# 🟠 STEP 4.5 — Launch EC2 Instance for Testing

1. Search **EC2**
2. Click **Launch Instance**
   ![](https://github.com/user-attachments/assets/70f81f71-b152-4b00-8703-10f468453561)

---

## Enter EC2 Details:
| Field | Value |
|-------|--------|
| Name | MACHINE1 |
| AMI | Amazon Linux |
| Instance Type | t3.micro |
| Key Pair | LONDON |
| VPC | Default |
| Subnet | Default |

Click **Launch Instance**  
![](https://github.com/user-attachments/assets/da9a6fc6-62b8-449c-aa30-ef853730e9a4)

![](https://github.com/user-attachments/assets/96437547-67fa-4cbd-82ca-38adfc0eedce)

---

# 🟠 STEP 4.6 — Update EC2 Security Group

1. Open **Security Groups**
2. Select EC2 SG
3. Click **Edit Inbound Rules**
   ![](https://github.com/user-attachments/assets/e1d90d64-6e1a-44d3-8bf9-54e9b08d73d7)

---

## Add Rule:
| Type | Source |
|------|---------|
| All Traffic | Anywhere (0.0.0.0/0) |

Click **Save Rules**  
![](https://github.com/user-attachments/assets/a4e14443-739e-4345-b12f-3e2eb17df20e)

---

# 🟠 STEP 4.7 — Connect to EC2

1. Select EC2 instance  
2. Click **Connect**
   ![](https://github.com/user-attachments/assets/189cc13a-1880-494a-aee9-fccb6523edcd)

3. Click **Connect** again  
   ![](https://github.com/user-attachments/assets/69fb46b5-ebe6-4687-9bea-0957f6b22c76)


---

# 🟪 PART 5 — Create Local Network Gateway + Azure VPN Connection

In this step, we map AWS network information into Azure and establish the Site-to-Site VPN tunnel.

---

# 🟣 STEP 5.1 — Create Local Network Gateway (LNG)

## 1️⃣ Open Local Network Gateway
1. Click **Search**
2. Type **LNG**
3. Select **Local Network Gateway**
   ![](https://github.com/user-attachments/assets/14aad5fe-827c-4e28-be98-dff5b707d676)

---

## 2️⃣ Create New Local Network Gateway
1. Click **Create**
   ![](https://github.com/user-attachments/assets/a64dc2d8-90fb-4336-9c88-d1992c807718)

---

## 3️⃣ Enter LNG Details
| Field | Value |
|-------|--------|
| Resource Group | PRATHAM |
| Region | Central India |
| Name | LNG |
| IP Address | `3.8.76.122` *(AWS Tunnel 1 Outside IP)* |
| Address Space | `172.31.0.0/16` *(AWS VPC CIDR)* |

![](https://github.com/user-attachments/assets/fc604513-5a8d-4dee-97c9-ca9c6339fb11)

Click **Review + Create → Create**  
![](https://github.com/user-attachments/assets/b9a1c48d-ebec-4e52-be77-ce19a3f59cbb)

---

# 🟣 STEP 5.2 — Create VPN Connection (Azure ↔ AWS)

## 1️⃣ Open Your Virtual Network Gateway (VNG)

1. Go to **Virtual Network Gateway**
2. Select **VNG**  
3. Click **Connections**
4. Click **Add**
   ![](https://github.com/user-attachments/assets/71ad0d95-a46a-4742-b4d8-fd90057e52ba)

---

## 2️⃣ Enter Connection Details

| Field | Value |
|-------|--------|
| Connection Type | Site-to-Site (IPSec) |
| Name | VNG-CONNECTION |
| Region | Central India |

Click **Next: Settings**
![](https://github.com/user-attachments/assets/e14ed389-32eb-4adf-ae1d-5b978c798545)

---

## 3️⃣ Configure VPN Connection

| Setting | Value |
|---------|--------|
| Virtual Network Gateway | VNG |
| Local Network Gateway | LNG |
| Authentication | Shared Key |
| Shared Key | *(Paste shared key from AWS Tunnel)* |
| IPSec/IKE Policy | Custom |
| IKE Phase 1 | Match AWS settings |
| IKE Phase 2 | Match AWS settings |

![](https://github.com/user-attachments/assets/ef8bd6bb-314a-45c0-86cd-03bb435541aa)

![](https://github.com/user-attachments/assets/1aa6c27b-55dd-4f34-bdf4-9f784444076a)

---

## 4️⃣ Review and Create
1. Click **Review + Create**
2. Click **Create**
   ![](https://github.com/user-attachments/assets/4ccefe73-6a76-4cd6-94e0-645078f6187c)

---

# 🟩 PART 5.3 — Testing VPN Connectivity

## Test from AWS EC2 → Azure VM

1. Connect to EC2 instance
2. Run command: `ping 10.0.1.4`

*(Replace with Azure VM’s private IP)*

![](https://github.com/user-attachments/assets/0ac8a7a3-6ddf-4262-af23-8c447a283ce4)

### ✔ If ping is successful  
The **Site-to-Site VPN is fully working**.

---

# 🎉 FINAL RESULT  

You have successfully created:

- Azure VNet + Subnets  
- Azure VM + NSG  
- Azure Virtual Network Gateway  
- AWS VGW + CGW  
- AWS VPN Connection  
- AWS Route Table updates  
- EC2 test instance  
- Local Network Gateway  
- Azure VPN Connection  
- Verified full connectivity  

This completes the **Azure ↔ AWS Site-to-Site VPN Lab** 🚀

---
# 👑 Author  
**Pratham**




