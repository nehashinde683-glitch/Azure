# 🌐 Azure Private DNS Lab

## 🎯 **LAB GOAL**
This lab demonstrates how to configure **Azure Private DNS** and resolve custom domain names inside a Virtual Network (VNet).  
You will learn to:

- Create Azure VNet and Subnets  
- Deploy a Windows Server VM  
- Install IIS Web Server & host a webpage  
- Create a Private DNS Zone  
- Link VNet to DNS Zone  
- Create DNS A-Record  
- Access the web server using internal FQDN  
- Test DNS resolution inside Azure  

---

# 🟦 **STEP 1 — Create Azure VNet and Subnet**

## 1️⃣ Open Virtual Network
1. Click **Virtual Network**  
   ![](https://github.com/user-attachments/assets/2dcf4737-eeef-4f7b-a937-384088b47e7c)

2. Click **Create**  
   ![](https://github.com/user-attachments/assets/0bc6c4c7-6125-4c83-ac9e-ef2ed43b3b12)

---

## 2️⃣ Enter VNet Details
| Field | Value |
|-------|-------|
| Resource Group | PRATHAM |
| VNet Name | V-NET |
| Region | Central India |

3. Click **IP Addresses**  
   ![](https://github.com/user-attachments/assets/df530974-4075-4218-93af-283e90dd3c5c)

---

## 🔹 Create Subnet
4. Click **Add Subnet**  
5. Subnet Purpose: **Default**  
6. Name: **VM-SUB**  
7. Starting Address: `10.0.1.0`  
8. Subnet Size: `/24`  
9. Click **Add**  

   ![](https://github.com/user-attachments/assets/31cfd727-1b38-4d56-98e5-e3b9ff1b0543)

---

# 🟩 **STEP 2 — Create Azure VM**

## 1️⃣ Open Virtual Machines
1. Click **Virtual Machines**  
   ![](https://github.com/user-attachments/assets/fd0a190b-138d-4b66-b1e4-c92879221440)
2. Click **Create → Virtual Machine**  
   ![](https://github.com/user-attachments/assets/1f4b89f9-d058-4b02-87a4-edf2ffba454b)

---

## 2️⃣ Enter VM Details
| Field | Value |
|-------|--------|
| Resource Group | PRATHAM |
| VM Name | VM-1 |
| Region | Central India |
| AZ | 1 |
| Image | Windows Server |
| Size | Standard_D2as_v5 (2 vCPU, 8GB RAM) |

![](https://github.com/user-attachments/assets/c36586f6-ff1e-4e6c-ac15-ac091d5b93a9)

---

## 3️⃣ Administrator Credentials
- Username: **VM-1**
- Password: `*******`
- Inbound Port: **RDP (3389)**

![](https://github.com/user-attachments/assets/e3c34404-e6de-49ad-a725-20a906edb901)

---

## 4️⃣ Networking Settings
- VNet: **V-NET**
- Subnet: **VM-SUB**

![](https://github.com/user-attachments/assets/c49423b6-b6a5-49d9-b200-159d82dec072)

Click **Review + Create → Create**  
![](https://github.com/user-attachments/assets/b489d514-50db-4ae7-bf6e-0d84c035689c)

---

# 🛡 **STEP 2A — Add NSG Rule (HTTP Allow)**

1. Go to **VM → Networking**  
   ![](https://github.com/user-attachments/assets/c0837a10-d834-470f-a3d8-48e9d609b70c)

2. Click **Create port rule → Inbound port rule**  
   ![](https://github.com/user-attachments/assets/b5948280-c155-40cc-b231-6f15ef8304bf)

### Add Rule
| Field | Value |
|-------|--------|
| Source | Any |
| Source Port | * |
| Destination | Any |
| Service | HTTP |
| Port | 80 |
| Protocol | TCP |
| Priority | 20 |
| Name | HTTP |

![](https://github.com/user-attachments/assets/6b075b29-4e32-4f5c-99ff-0d41f5cf648a)

---

# 🟦 **STEP 2B — Connect to VM Using RDP**

1. Go to VM → Overview → Copy Public IP  
   ![](https://github.com/user-attachments/assets/e96883d2-6192-4d4c-87c7-62eecdd8a007)

2. Open **Remote Desktop Connection**  
   ![](https://github.com/user-attachments/assets/54901e48-daf7-440f-8a69-a8d2b2465720)

3. Enter Public IP  
4. Login  
5. Click YES  
   ![](https://github.com/user-attachments/assets/372c55d1-95da-408a-b8cd-31f58a69d931)

---

# 🔥 **STEP 2C — Turn OFF Windows Firewall (Lab Only)**

⚠️ *Only for testing DNS / ping.*

1. Press **Windows + R** → type `firewall.cpl`  
   ![](https://github.com/user-attachments/assets/f98bb8dd-2dd7-4686-aefe-cb3b1dbb2bf1)

2. Click **Turn Windows Firewall on or off**  
   ![](https://github.com/user-attachments/assets/6366a21c-025e-4719-a0f5-15d854307148)

3. Turn OFF both **Private** and **Public** firewall  
   ![](https://github.com/user-attachments/assets/2ebbb8f5-1d7e-4cb1-ad73-e496b5d38cfb)

---

# 🟧 **STEP 2D — Install IIS Web Server**

1. Open **Server Manager**  
   ![](https://github.com/user-attachments/assets/0798d6b6-f6f9-42fb-907e-6b8a5abeeafb)

2. Click **Add roles and features**  
   ![](https://github.com/user-attachments/assets/c2ba03f7-8307-48de-9e09-09ef3b7ea5a7)

3. Select **Web Server (IIS)**  
   ![](https://github.com/user-attachments/assets/5c6e66f3-9c1b-493c-b2c8-3fa7b20e3a7c)

4. Click **Install**  
   ![](https://github.com/user-attachments/assets/f1d60bd5-1e32-4d81-a742-4c640f206108)

---

# 🟧 Create `index.html`

1. Open **File Explorer**  
2. Go to:  `C:\inetpub\wwwroot`
   ![](https://github.com/user-attachments/assets/6c5d3191-65e7-4fe8-948e-11c63f3a7c5b)

3. Delete default files  
4. Create **index.html**  
5. Add content:  `WELCOME TO SERVER 1`
   
![](https://github.com/user-attachments/assets/d2b8e60b-ddc8-4883-9735-bac5962c29f3)

---

# 🟪 STEP 3 — Create Private DNS Zone

1. Search → **Private DNS Zones**  
![](https://github.com/user-attachments/assets/20a84156-35fb-4647-9e09-8b4e832f9504)

2. Click **Create**

3. Basic Settings  
| Field | Value |
|-------|--------|
| Resource Group | PRATHAM |
| DNS Zone Name | pratham.in |

![](https://github.com/user-attachments/assets/7d2cfae1-71aa-4fe6-a0e8-e8caaf13b586)

---

## Link VNet with Private DNS Zone

1. Go to **Virtual Network Links**  
2. Click **Add**  
3. Name: `DNS-LINK`  
4. Select VNet: **V-NET**  
5. Enable Auto Registration  
6. Click Create  

![](https://github.com/user-attachments/assets/c4bc4dfa-ffcf-47b8-a097-0ac111707d51)  
![](https://github.com/user-attachments/assets/540da18c-6019-4f1a-a8b3-ec717dd960a5)

---

# 🟫 STEP 3B — Create DNS A-Record

1. Open **pratham.in** DNS zone  
2. Go to **Record Set**  
3. Click **Add Record**  
![](https://github.com/user-attachments/assets/3fe1ddbf-c259-4266-bd39-13b1972fc21c)

4. Fill details:
   
| Field | Value |
|------|--------|
| Name | www |
| Type | A |
| IP | 10.0.1.4 (VM Private IP) |

5. CLICK ON ADD

   <img width="1919" height="1078" alt="image" src="https://github.com/user-attachments/assets/014914c2-e663-4095-b7c7-e887bbf3e310" />

---

# 🟩 STEP 4 — Testing Private DNS

1. Open browser inside VM  
2. Type:  `www.pratham.in`
3. Website should load using internal DNS  
![](https://github.com/user-attachments/assets/f09a3490-1c7e-4a45-b244-3902a5b54a60)

---

# 🎉 **LAB COMPLETED SUCCESSFULLY**

You have configured:

✔ VNet + Subnet  
✔ Windows VM + IIS  
✔ Private DNS Zone  
✔ VNet Link + Auto-Registration  
✔ DNS A-Record  
✔ Private DNS Resolution Working  

---

# 👑 Author  
**Pratham**

