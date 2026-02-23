
# 🟦 Create Azure VNet and Subnets and cread vm in web server in windod machine

---
# stape 1 create vnet and subnet

## 1️⃣ Open Virtual Network

1. Go to Azure Portal  
2. Click on **Virtual Network** icon  
   ![](https://github.com/user-attachments/assets/2dcf4737-eeef-4f7b-a937-384088b47e7c)

3. Click **Create**  
   ![](https://github.com/user-attachments/assets/0bc6c4c7-6125-4c83-ac9e-ef2ed43b3b12)

---

## 2️⃣ Enter VNet Details

- **Resource Group:** `PRATHAM`
- **Name:** `V-NET`
- **Region:** `Central India`

4. Click **IP Addresses**  
   ![](https://github.com/user-attachments/assets/df530974-4075-4218-93af-283e90dd3c5c)

---

## 🔹 Create Subnet

5. Click **Add Subnet**  
6. Subnet Purpose: **Default**  
7. Name: `VM-SUB`  
8. Starting Address: `10.0.1.0`  
9. Subnet Size: `/24`  
10. Click **Add**  

   ![](https://github.com/user-attachments/assets/31cfd727-1b38-4d56-98e5-e3b9ff1b0543)

---

## ✅ Review and Create VNet

11. Click **Review + Create**  
    <img width="1919" height="1079" src="https://github.com/user-attachments/assets/31f2cc04-04d3-4028-a410-8553ed7ca7b9" />

12. Click **Create**  
    <img width="1918" height="1077" src="https://github.com/user-attachments/assets/4d6a8493-a2a5-408f-a3d8-b8bc7c90b7b1" />

⏳ **It will take 2–3 minutes for deployment**

---
## create vm in vnet
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
