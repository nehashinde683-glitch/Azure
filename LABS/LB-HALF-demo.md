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

# 🔹 Create Subnet 

4. Click **Add Subnet**  
5. Subnet Purpose: **Default**  
6. Name: **VM-SUB**  
7. Starting Address: `10.0.1.0`  
8. Subnet Size: `/24`  
9. Click **Add**  

   ![](https://github.com/user-attachments/assets/31cfd727-1b38-4d56-98e5-e3b9ff1b0543)

---


# 🟩 STEP 2 — Create Azure VM

## VM-1

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



## VM-2
## 1️⃣ Open Virtual Machines
1. Click **Virtual Machines**  
   ![](https://github.com/user-attachments/assets/fd0a190b-138d-4b66-b1e4-c92879221440)

2. Click **Create**  
  <img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/5c448132-a98a-4bf8-951d-7de349455ff5" />

---
## 2️⃣ Enter VM Details
- Resource Group: **PRATHAM**
- VM Name: **VM-2**
- Region: **Central India**
- Availability Zone: **1**
- Image: **Windows Server**
- Size: **Standard_D2as_v5 (2 vCPUs, 8 GB RAM)**

<img width="1919" height="1077" alt="image" src="https://github.com/user-attachments/assets/de351d23-f135-4d1a-9f31-9cd2a5a90688" />
<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/d3c759e8-a6e5-443a-9eab-9c2acc48f7fd" />


---
## 3️⃣ Administrator Account
- Username: **VM-2**
- Password: `*******`
- Inbound Port: **RDP (3389)**

<img width="1919" height="1078" alt="image" src="https://github.com/user-attachments/assets/1fa89043-2148-4451-8e2b-446ec89d39ec" />

---
## 4️⃣ Networking Settings
- Virtual Network: **V-NET**
- Subnet: **VM-SUB**

<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/ad728202-5274-4064-8d74-0ae279c34cb8" />

Click **Review + Create → Create**  
<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/08835452-65e6-440f-a097-db3a8cc23805" />


---

# 🛡 STEP 3 — Add NSG Inbound Rule (HTTP Example)

## VM-1

1. Go to **VM-1 → Networking**  
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
| Priority | 200 |
| Name | HTTP |

![](https://github.com/user-attachments/assets/6b075b29-4e32-4f5c-99ff-0d41f5cf648a)

---
## VM-2

1. Go to **VM-2 → Networking**  
  <img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/9699bba1-0e88-4848-9abb-ba5759413c9f" />

2. Click **Create port rule**  
3. Select **Inbound port rule**  
   <img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/2630f13e-cd66-45ac-ad81-c26370e37068" />


### Add Rule:
| Field | Value |
|-------|-------|
| Source | Any |
| Source Port | * |
| Destination | Any |
| Service | HTTP |
| Destination Port | 80 |
| Protocol | TCP |
| Priority | 200 |
| Name | HTTP |

<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/4c584dc4-c606-4ac3-9a75-0ec6f842a0c1" />

---


# 🟦 STEP 4 — Connect to Azure VM-1 (via RDP)

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

# 🔥 STEP 5 — Turn OFF Windows Firewall 
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

### install role web server iis
1. clickon window icone
2. click on server manager
   <img width="1918" height="1078" alt="image" src="https://github.com/user-attachments/assets/0798d6b6-f6f9-42fb-907e-6b8a5abeeafb" />
3. click on add features and role
   <img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/c2ba03f7-8307-48de-9e09-09ef3b7ea5a7" />
4. go to server role
5. select web server (iis)
6. click on next
   <img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/5c6e66f3-9c1b-493c-b2c8-3fa7b20e3a7c" />
7. click on install
   <img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/f1d60bd5-1e32-4d81-a742-4c640f206108" />

### add index.ttml file
1. click on window icone
2. click on file Explorer
   <img width="1919" height="1077" alt="image" src="https://github.com/user-attachments/assets/6c5d3191-65e7-4fe8-948e-11c63f3a7c5b" />
3. go to this pc -- go to windows c -- initpub -- wwwroot
4. remove by defalte file
5. create index.html file
6. type WELCOME TO SERVER 1
   <img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/d2b8e60b-ddc8-4883-9735-bac5962c29f3" />

### SAME FOR VM-2
1. CONNECT TO VM-2 VIA RDB
2. Turn OFF Windows Firewall
   <img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/5fa127d6-a9bb-4e9f-ab38-4238cb4da893" />
4. install role web server iis
   <img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/8df0301e-66b2-4949-8620-fe5e102e765c" />
6. add index.html file
   <img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/1be1302d-b43b-4473-83bc-917bf0bbaf0e" />

## stap 6 create lb 
1. srarch lb
2. click on load balancer icone
   <img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/51db61b3-c188-437d-bce6-cff912babfa7" />
3. CHOICE RESOURCE GROUP: `PRATHAM`
4. TYPE NAME: `LB`
5. SELECT REGION: `CENTRAL INDIA`
6. SKU : `Standard (Distribute traffic to backend resources)`
7. TYPE : `PUBLIC`
8. TIER : `Globle`
9. CLICK NEXT:FRONTEND IP CONFIGURATION
   <img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/ad3020ac-f02e-4506-910f-91abd5118e71" />

10. ADD FRONTEND IP CONFIGURATION
    1. NAME: `LB-FD`
    2. IP VERSION: `IPV4`
    3. IP TYPE IP : `ADDRESS`
    4. PUBLIC IP ADDRESS: `CLICK CREATE NEW`
11. ADD A PUBLIC IP ADDRESS
    1. NAME: `FD-IP`
    2. SAVE --- SAVE
    3. REWIEW + CREATE
<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/bfb327c6-5e7c-45a7-b451-26580047d3fe" />



    #LB HALF 
