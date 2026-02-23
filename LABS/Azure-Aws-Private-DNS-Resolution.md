# Azure–AWS Site-to-Site VPN with Private DNS & DNS Resolvers

## 🎯 Lab Goal

This lab is to connect **Azure** and **AWS** using a secure
**Site-to-Site VPN** and set up **private DNS resolution** between both clouds.

By completing this lab, you will learn how to:

- Create an Azure VNet, subnets, and a Virtual Machine  
- Create an Azure VPN Gateway  
- Configure AWS VPC, VGW, CGW, and VPN Connection  
- Build a working VPN tunnel between Azure and AWS  
- Test communication using private IP ping  
- Create an Azure Load Balancer and host a web page  
- Create a Private DNS Zone in Azure  
- Configure Azure DNS Private Resolver  
- Configure AWS Route53 Outbound Resolver  
- Test DNS name resolution from AWS to Azure using `curl www.pratham.in`

This lab helps you understand **multi-cloud networking**, **VPN**, and **private DNS** in a very simple and practical way.


# 🟦 STEP 1 — Create Azure VNet and Subnets

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

---

# ✅ Review and Create VNet

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

# 🛡 STEP 2A — Add NSG Inbound Rule (HTTP)

1. Go to **VM → Networking**  
   ![](https://github.com/user-attachments/assets/c0837a10-d834-470f-a3d8-48e9d609b70c)

2. Click **Create port rule**  
3. Click **Inbound port rule**  
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

1. Go to VM → Overview  
2. Copy **Public IP**  
   ![](https://github.com/user-attachments/assets/e96883d2-6192-4d4c-87c7-62eecdd8a007)

3. Open **Remote Desktop Connection**  
   ![](https://github.com/user-attachments/assets/54901e48-daf7-440f-8a69-a8d2b2465720)

4. Enter Public IP  
   ![](https://github.com/user-attachments/assets/8a4d9413-7ab5-4902-941a-1dac9d5be47c)

5. Login:  
   - Username: **VM-1**  
   - Password: `*******`

6. Click **Yes**  
   ![](https://github.com/user-attachments/assets/372c55d1-95da-408a-b8cd-31f58a69d931)

---

# 🔥 STEP 2C — Turn OFF Windows Firewall (LAB ONLY)

1. Press **Windows + R**  
2. Type `firewall.cpl`  
3. Click OK  
   ![](https://github.com/user-attachments/assets/f98bb8dd-2dd7-4686-aefe-cb3b1dbb2bf1)

4. Click **Turn Windows Defender Firewall on or off**  
   ![](https://github.com/user-attachments/assets/6366a21c-025e-4719-a0f5-15d854307148)

5. Turn OFF:
- Private firewall  
- Public firewall  

![](https://github.com/user-attachments/assets/2ebbb8f5-1d7e-4cb1-ad73-e496b5d38cfb)

---

# 🌐 STEP 2D — Install IIS Web Server

1. Open **Server Manager**  
   ![](https://github.com/user-attachments/assets/0798d6b6-f6f9-42fb-907e-6b8a5abeeafb)

2. Click **Add roles and features**  
   ![](https://github.com/user-attachments/assets/c2ba03f7-8307-48de-9e09-09ef3b7ea5a7)

3. Go to **Server Roles**  
4. Select **Web Server (IIS)**  
   ![](https://github.com/user-attachments/assets/5c6e66f3-9c1b-493c-b2c8-3fa7b20e3a7)

5. Click **Install**  
   ![](https://github.com-user-attachments/assets/f1d60bd5-1e32-4d81-a742-4c640f206108)

---

# 📝 STEP 2E — Create index.html Page

1. Open **File Explorer**  
   ![](https://github.com/user-attachments/assets/6c5d3191-65e7-4fe8-948e-11c63f3a7c5b)

2. Navigate to:  
   **This PC → Windows (C:) → inetpub → wwwroot**

3. Delete default files  
4. Create new file: **index.html**  
5. Add text:

```
WELCOME TO SERVER 1
```

![](https://github.com/user-attachments/assets/d2b8e60b-ddc8-4883-9735-bac5962c29f3)

---
# 🟦 STEP 3 — Create Azure Virtual Network Gateway (VNG)

---

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
| Resource Group | **PRATHAM** |
| Name | **VNG** |
| Region | **Central India** |
| Gateway Type | **VPN** |
| VPN Type | **Route-based** |
| SKU | **VpnGw1 (recommended)** |
| Virtual Network | **V-NET** |
| Subnet | **GatewaySubnet** |
| Public IP | Create new → **VNG-PUB-IP** |

![](https://github.com/user-attachments/assets/c4729370-e52a-4408-ac11-91e16248fbe8)

---

## 4️⃣ Disable Unnecessary Options

| Option | Value |
|--------|--------|
| Active-Active Mode | **Disabled** |
| BGP | **Disabled** |

![](https://github.com/user-attachments/assets/903ed485-a74a-4aea-8efa-2791910e5807)

---

## 5️⃣ Review and Create

1. Click **Review + Create**
2. Click **Create**

⏳ *Note: VNG creation takes approximately **20–30 minutes**.*

---
# 🟧 STEP 4 — AWS VPC Configuration  
This section covers all AWS components required to establish the Site-to-Site VPN connection with Azure.

You will configure:
- Virtual Private Gateway (VGW)  
- Customer Gateway (CGW)  
- Site-to-Site VPN Connection  
- Route Tables  
- EC2 Instance for testing  
- EC2 Security Group  

---

# 🟠 STEP 4.1 — Create Virtual Private Gateway (VGW)

## 1️⃣ Open AWS Console → Search "VPC"

![](https://github.com/user-attachments/assets/6fd5be68-4138-4ffa-bbc4-a484da2df406)

---

## 2️⃣ Go to **Virtual Private Gateways**
1. Click **Virtual Private Gateways**
2. Click **Create Virtual Private Gateway**

![](https://github.com/user-attachments/assets/514265da-29cf-4097-a4d8-4a2738deb3b3)

---

## 3️⃣ Enter Details

| Field | Value |
|-------|--------|
| Name | **VPG** |
| ASN | **Default** |

Click **Create Virtual Private Gateway**

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

1. Click **Customer Gateways**
2. Click **Create Customer Gateway**

![](https://github.com/user-attachments/assets/83482745-13dd-4d46-84d9-26cc4901f3de)

---

## Enter Details

| Field | Value |
|-------|--------|
| Name | **AZURE-CGW-TO-AWS** |
| IP Address | **4.224.72.113** *(Azure VNG Public IP)* |
| Routing | **Static** |

Click **Create Customer Gateway**

![](https://github.com/user-attachments/assets/8965b5ba-393f-4cc5-80b3-ffb62f50693a)

---

# 🟠 STEP 4.3 — Create Site-to-Site VPN Connection

1. Open **Site-to-Site VPN Connections**
2. Click **Create VPN Connection**

![](https://github.com/user-attachments/assets/aeec08c5-f3d0-411a-a766-6704e74c842c)

---

## Enter Details

| Field | Value |
|-------|--------|
| Name | **VPN** |
| Virtual Private Gateway | **VPG** |
| Customer Gateway | **AZURE-CGW-TO-AWS** |
| Routing | **Static** |
| Static Prefix | **10.0.0.0/16** *(Azure VNet)* |

Click **Create VPN Connection**

![](https://github.com/user-attachments/assets/010f4599-d40a-4370-ab8e-4f87bd5620a3)

![](https://github.com/user-attachments/assets/fa658c61-84db-47d3-8f64-c4712a0a7d49)

---

# 🟠 STEP 4.4 — Update AWS Route Table

1. Open **Route Tables**
2. Select Default Route Table
3. Click **Edit Routes**

![](https://github.com/user-attachments/assets/ce4b217e-39eb-4222-893b-cd9dad2298d3)

---

## Add Route

| Destination | Target |
|-------------|--------|
| **10.0.0.0/16** | **Virtual Private Gateway (VPG)** |

Click **Save Changes**

![](https://github.com/user-attachments/assets/4eb728c2-d44f-44fe-83ce-db588544e15b)

---

# 🟠 STEP 4.5 — Launch EC2 Instance (Testing Machine)

1. Search **EC2**
2. Click **Launch Instance**

![](https://github.com/user-attachments/assets/70f81f71-b152-4b00-8703-10f468453561)

---

## Enter EC2 Details

| Field | Value |
|-------|--------|
| Name | **MACHINE1** |
| AMI | **Amazon Linux** |
| Instance Type | **t3.micro** |
| Key Pair | **LONDON** |
| VPC | **Default VPC** |
| Subnet | **Default Subnet** |

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

## Add Rule

| Type | Source |
|------|---------|
| **All Traffic** | **0.0.0.0/0** |

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

# 🟪 STEP 5 — Azure Local Network Gateway + VPN Connection

In this step, you will:

- Create Local Network Gateway (LNG)  
- Create VPN Connection between Azure VNG ↔ AWS VGW  
- Apply Shared Key  
- Match IPSec/IKE settings  
- Validate tunnel status  

---

# 🟣 STEP 5.1 — Create Local Network Gateway (LNG)

## 1️⃣ Open Local Network Gateway
1. Click **Search**
2. Type **Local Network Gateway**
3. Select it

![](https://github.com/user-attachments/assets/14aad5fe-827c-4e28-be98-dff5b707d676)

---

## 2️⃣ Click **Create**

![](https://github.com/user-attachments/assets/a64dc2d8-90fb-4336-9c88-d1992c807718)

---

## 3️⃣ Enter LNG Details

| Field | Value |
|-------|--------|
| Resource Group | **PRATHAM** |
| Region | **Central India** |
| Name | **LNG** |
| IP Address | `3.8.76.122` *(AWS Tunnel #1 Outside IP)* |
| Address Space | `172.31.0.0/16` *(AWS VPC CIDR)* |

![](https://github.com/user-attachments/assets/fc604513-5a8d-4dee-97c9-ca9c6339fb11)

---

## 4️⃣ Click **Review + Create → Create**

![](https://github.com/user-attachments/assets/b9a1c48d-ebec-4e52-be77-ce19a3f59cbb)

---

# 🟣 STEP 5.2 — Create VPN Connection (Azure ↔ AWS)

## 1️⃣ Open your **Virtual Network Gateway (VNG)**

1. Go to **Virtual Network Gateway**
2. Click **VNG**

---

## 2️⃣ Open **Connections** → Click **Add**

![](https://github.com/user-attachments/assets/71ad0d95-a46a-4742-b4d8-fd90057e52ba)

---

## 3️⃣ Enter Connection Details

| Field | Value |
|-------|--------|
| Connection Type | **Site-to-Site (IPSec)** |
| Name | **VNG-CONNECTION** |
| Region | **Central India** |

![](https://github.com/user-attachments/assets/e14ed389-32eb-4adf-ae1d-5b978c798545)

Click **Next: Settings**

---

## 4️⃣ Configure VPN Settings

| Setting | Value |
|---------|--------|
| Virtual Network Gateway | **VNG** |
| Local Network Gateway | **LNG** |
| Authentication | **Shared Key** |
| Shared Key | *(Paste Shared Key from AWS VPN Tunnel)* |
| IPSec/IKE Policy | **Custom** |

👇 AWS IKE settings must match here.

![](https://github.com/user-attachments/assets/ef8bd6bb-314a-45c0-86cd-03bb435541aa)

![](https://github.com/user-attachments/assets/1aa6c27b-55dd-4f34-bdf4-9f784444076a)

---

## 5️⃣ Review + Create

![](https://github.com/user-attachments/assets/4ccefe73-6a76-4cd6-94e0-645078f6187c)

---

# 🟩 STEP 5.3 — Testing VPN Connectivity

## 1️⃣ Connect to AWS EC2

1. Select EC2 instance  
2. Click **Connect**

![](https://github.com/user-attachments/assets/189cc13a-1880-494a-aee9-fccb6523edcd)

3. Click **Connect** again

![](https://github.com/user-attachments/assets/69fb46b5-ebe6-4687-9bea-0957f6b22c76)

---

## 2️⃣ Ping Azure VM Private IP

```
ping 10.0.1.4

```
![](https://github.com/user-attachments/assets/0ac8a7a3-6ddf-4262-af23-8c447a283ce4)

### ✔ If ping is successful  
The **Site-to-Site VPN is fully working**.

---
# 🟦 STEP 6 — Create Azure Load Balancer (Public LB)

Load Balancer distributes incoming traffic across backend VMs.  
Here we create:

- Public Load Balancer  
- Frontend IP  
- Backend Pool  
- Health Probe  
- Load Balancing Rule  

---

# 🟦 STEP 6.1 — Open Load Balancer Service

1. Search **Load Balancer**
2. Click the Load Balancer icon

![](https://github.com/user-attachments/assets/51db61b3-c188-437d-bce6-cff912babfa7)

---

# 🟦 STEP 6.2 — Create Load Balancer

1. Click **Create**
2. Select **Standard Load Balancer**

![](https://github.com/user-attachments/assets/30a0b6ff-eb61-4da5-8cce-b16cb6fc885d)

### Fill the details:

| Field | Value |
|--------|--------|
| Resource Group | PRATHAM |
| Name | LB |
| Region | Central India |
| SKU | Standard |
| Type | Public |
| Tier | Regional |

Click **Next: Frontend IP Configuration**

---

# 🟦 STEP 6.3 — Create Frontend IP

1. Click **Add Frontend IP Configuration**
2. Fill:

| Field | Value |
|--------|--------|
| Name | LB-FD |
| IP Version | IPv4 |
| IP Type | Public |
| Public IP | Create New |

---

### Create Public IP Address

| Field | Value |
|--------|--------|
| Name | FD-IP |

Click **Save** → Save again

![](https://github.com/user-attachments/assets/82916f0b-0f85-468f-b161-2977240acc86)

Click **Review + Create → Create**

![](https://github.com/user-attachments/assets/230804b7-2982-4ffe-b2fa-dc101c56cf22)

---

# 🟦 STEP 6.4 — Create Backend Pool

1. Open **LB**
2. Go to **Backend Pools**
3. Click **Add**

![](https://github.com/user-attachments/assets/8fb45f19-5d0b-49de-8bc2-182824b3effc)

### Fill:

| Field | Value |
|--------|--------|
| Name | LB-BP |
| Virtual Network | V-NET |
| Backend Pool Configuration | NIC |

4. Click **Add**
5. Select VM → **VM-1**
6. Click **Add**
7. Click **Save**

![](https://github.com/user-attachments/assets/c18e9842-4ba8-4336-a56e-89b3861ffa5f)

---

# 🟦 STEP 6.5 — Create Health Probe

1. Inside **LB**
2. Go to **Health Probes**
3. Click **Add**

![](https://github.com/user-attachments/assets/52c61a61-c8c5-49a9-a9e4-8d71d7d46039)

### Fill:

| Field | Value |
|--------|--------|
| Name | LB-HP |
| Protocol | HTTP |
| Port | 80 |

Click **Save**

![](https://github.com/user-attachments/assets/965df74e-107d-49ee-b34b-7802d983f618)

---

# 🟦 STEP 6.6 — Create Load Balancer Rule

1. Go to **Load Balancing Rules**
2. Click **Add**

![](https://github.com/user-attachments/assets/90f6e49d-c8ca-4560-98df-6a9e241a4c35)

---

### Fill Rule Details:

| Field | Value |
|--------|--------|
| Name | LB-RULE |
| IP Version | IPv4 |
| Frontend IP | LB-FD |
| Backend Pool | LB-BP |
| Protocol | TCP |
| Port | 80 |
| Backend Port | 80 |
| Health Probe | LB-HP |

Click **Save**

![](https://github.com/user-attachments/assets/971c8d32-f59e-461c-a712-c2dbc2e5fd5a)

---

# 🟪 STEP 7 — Create Private DNS Zone in Azure

Private DNS Zone allows VMs inside Azure or hybrid networks to resolve domain names
(e.g., **www.pratham.in**) to **private IP addresses**.

In this step we will:

- Create a Private DNS Zone  
- Link the VNet with Auto Registration  
- Create A-Record for Load Balancer  

---

# 🟪 STEP 7.1 — Open Private DNS Zone Service

1. Search **Private DNS Zones**
2. Click on the service icon

![](https://github.com/user-attachments/assets/20a84156-35fb-4647-9e09-8b4e832f9504)

---

# 🟪 STEP 7.2 — Create Private DNS Zone

1. Click **Create**
2. Fill in the following:

| Field | Value |
|--------|--------|
| Resource Group | PRATHAM |
| DNS Zone Name | pratham.in |

![](https://github.com/user-attachments/assets/7d2cfae1-71aa-4fe6-a0e8-e8caaf13b586)

Click **Next → Review + Create → Create**

---

# 🟪 STEP 7.3 — Link DNS Zone with Virtual Network

1. Inside the DNS Zone → Click **Virtual network links**
2. Click **Add**

Fill details:

| Field | Value |
|--------|--------|
| Name | DNS-LINK |
| Virtual Network | V-NET |
| Auto Registration | Enabled |

![](https://github.com/user-attachments/assets/c4bc4dfa-ffcf-47b8-a097-0ac111707d51)

Click **Create**

![](https://github.com/user-attachments/assets/540da18c-6019-4f1a-a8b3-ec717dd960a5)

---

# 🟪 STEP 7.4 — Create DNS A-Record (www → Load Balancer IP)

1. Open **pratham.in** DNS Zone
2. Click **Record Set**
3. Click **Add**

![](https://github.com/user-attachments/assets/3fe1ddbf-c259-4266-bd39-13b1972fc21c)

Fill record details:

| Field | Value |
|--------|--------|
| Name | www |
| Type | A |
| IP Address | 4.224.153.213 *(Load Balancer Public IP)* |

Click **Add**

![](https://github.com/user-attachments/assets/52f40657-418a-43a5-8082-ccab8ecebf19)

---

# 🟦 STEP 7E — Create DNS Private Inbound Resolver (Azure)

Azure DNS Private Resolver allows **on-prem / AWS / other networks** to resolve Azure Private DNS names
(e.g., **www.pratham.in**) by sending DNS queries to Azure via VPN.

In this step we create:

- DNS Private Resolver  
- Inbound Endpoint (AWS → Azure DNS queries)  
- Custom Subnet for Resolver  

---

# 🟦 STEP 7E.1 — Open DNS Private Resolver Service

1. Search **DNS Private Resolver**
2. Click the service icon

![](https://github.com/user-attachments/assets/f1202609-7d1a-428c-9f75-cd793e7eb0a4)

---

# 🟦 STEP 7E.2 — Create DNS Private Resolver

1. Click **Create**

![](https://github.com/user-attachments/assets/5e79a483-d6e3-4324-9f61-2218a8261a30)

Fill details:

| Field | Value |
|--------|--------|
| Resource Group | PRATHAM |
| Name | DNS-RESOLVER |
| Region | Central India |
| Virtual Network | V-NET |

Click **Next: Inbound endpoint**

![](https://github.com/user-attachments/assets/85e674da-d993-4047-9cc5-95a79153c263)

---

# 🟦 STEP 7E.3 — Create Inbound Endpoint

1. Click **Add inbound endpoint**

| Field | Value |
|--------|--------|
| Endpoint Name | DNS-INBD-ENDP |
| Subnet | Create New |

![](https://github.com/user-attachments/assets/845ae6d2-ee1a-4033-9d8d-7e37b604bfd2)

### Create Subnet for Resolver
| Field | Value |
|--------|--------|
| Name | DNS-INBD-SUB |
| Address Range | 10.0.4.0/24 |

Click **Create**

---

# 🟦 STEP 7E.4 — Configure Endpoint Settings

| Field | Value |
|--------|--------|
| IP Assignment | Dynamic |

Click **Save**

---

# 🟦 STEP 7E.5 — Review and Create

1. Click **Review + Create**

![](https://github.com/user-attachments/assets/112a77a1-f4c3-4e28-93d0-d7c3fb4b4d0b)

2. Click **Create**

![](https://github.com/user-attachments/assets/8cf84033-c549-4e23-a0a3-bdbcf774d51b)

---

# 🟧 STEP 8 — Create AWS Route 53 Outbound Resolver

AWS Route53 Outbound Resolver is required for:

✔ Forwarding AWS DNS queries → Azure DNS Private Resolver  
✔ Enabling EC2 instances to resolve Azure Private DNS names (e.g., **www.pratham.in**)  
✔ Completing cross-cloud DNS resolution in hybrid environment  

---

# 🟧 STEP 8.1 — Open Route 53

1. Search **Route 53** in AWS Console  
2. Click on **Route 53**

![](https://github.com/user-attachments/assets/edc83143-5161-4edf-a954-ac079eb6edd1)

---

# 🟧 STEP 8.2 — Create Outbound Resolver Endpoint

1. Go to **Outbound Endpoints**
2. Click **Create outbound endpoint**

![](https://github.com/user-attachments/assets/5890dd16-5281-48fe-9054-5aa158cf2e33)

---

## Fill Outbound Endpoint Details

| Field | Value |
|--------|--------|
| Endpoint Name | aws-endpoint |
| VPC | Default VPC |
| Security Group | Select default SG |
| Endpoint type | IPv4 |

![](https://github.com/user-attachments/assets/608ffd22-9d19-4314-b1ae-eec614d7c0a3)

---

# 🟧 STEP 8.3 — Configure IP Addresses (2 AZs)

### IP Address #1

| Field | Value |
|--------|--------|
| Availability Zone | eu-west-2a |
| Subnet | Default Subnet |

### IP Address #2

| Field | Value |
|--------|--------|
| Availability Zone | eu-west-2b |
| Subnet | Default Subnet |

![](https://github.com/user-attachments/assets/e5b7a0a4-f40f-48e8-97d1-af1237e61ca0)

---

# 🟧 STEP 8.4 — Create Outbound Endpoint

Click **Create outbound endpoint**

![](https://github.com/user-attachments/assets/409f45c3-6f5e-4c51-ba0d-db6e38e2f4bb)

---

# 🟧 STEP 8.5 — Create DNS Forwarding Rule

1. Go to **Rules** tab  
2. Click **Create rule**

![](https://github.com/user-attachments/assets/8c7336ce-39c0-4ebf-95ef-bc2a2060bf3c)

---

# 🟧 STEP 8.6 — Fill Rule Details

| Field | Value |
|--------|--------|
| Rule Name | OTBD-RULE |
| Rule Type | Forward |
| Domain Name | pratham.in |
| VPCs that use this rule | Default VPC |
| Outbound Endpoint | aws-endpoint |

![](https://github.com/user-attachments/assets/4a773336-f3d5-4fc6-bfe4-87aec544aef1)

---

# 🟧 STEP 8.7 — Add Target IP (Azure DNS Resolver)

| Field | Value |
|--------|--------|
| IPv4 Address | `10.0.4.4` |

⚠ This IP = Azure DNS Private Resolver **Inbound Endpoint** IP  
(Very important)

![](https://github.com/user-attachments/assets/17180776-61b4-4e37-a6b7-4570425cc70d)

Click **Submit**

---

# 🟩 STEP 9 — Testing DNS Resolution & Connectivity from AWS EC2

---

# 🟩 STEP 9.1 — Connect to EC2 Instance

1. Open **EC2 Dashboard**
2. Select the **MACHINE1** instance
3. Click **Connect**

![](https://github.com/user-attachments/assets/189cc13a-1880-494a-aee9-fccb6523edcd)

---

4. Click **Connect** again in the EC2 Connect window

![](https://github.com/user-attachments/assets/69fb46b5-ebe6-4687-9bea-0957f6b22c76)

5. Type
   ```
   curl www.pratham.in
   ```
   <img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/a3d50355-2079-41ec-b15b-757063772a69" />


---
