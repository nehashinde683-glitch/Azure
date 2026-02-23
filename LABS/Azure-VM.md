# 🖥️ Create Virtual Machine in Azure

This guide explains how to create a Windows virtual machine in Azure with step-by-step screenshots.

---
# 🧩 Architecture Diagram

<img width="1597" height="788" alt="Screenshot 2025-12-09 233130" src="https://github.com/user-attachments/assets/cd431030-386a-41e1-a747-730445297b9d" />

---

## 1️⃣ Go to Azure Portal
1. Visit **Azure Portal**
2. Sign in or create a new account
3. Click on **Virtual Machines**
   
<img width="1919" height="1079" src="https://github.com/user-attachments/assets/de609490-7617-49c5-9b93-4621831af172">

---

## 2️⃣ Start VM Creation
4. Click on **Create**
   
<img width="1919" height="1079" src="https://github.com/user-attachments/assets/1b1d9bce-1963-4c36-b076-90c2f6351863">

5. Select **Virtual Machine**

<img width="1919" height="1079" src="https://github.com/user-attachments/assets/afd4002b-045a-4ab4-8c45-8a48e92b4186">

---

## 3️⃣ Project Details
6. Fill project details  
   - **Resource Group:** Click *Create New*  
   - Name: `PRATHAM`  
   - Click **OK**

<img width="1919" height="1079" src="https://github.com/user-attachments/assets/38acb691-a194-4c97-bf96-eca4bf4875e8">

---

## 4️⃣ Instance Details
7. Configure VM:

- VM Name → `VM-1`
- Region → `Central India`
- Availability Zone → `Zone 1`
- Image → `Windows Server 2025`
- Size → `Standard_D2as_v5 (2 vcpus, 8 GiB RAM)`
- Username → `VM-1`
- Password → `********`
- Inbound Port → `3389` (for RDP)

<img width="1919" height="1079" src="https://github.com/user-attachments/assets/2d8358ea-40ec-45c2-be07-4a210d1f4b3d">

<img width="1914" height="1079" src="https://github.com/user-attachments/assets/fe20a1bf-9073-4b6a-93f0-4416086586bb">

---

## 5️⃣ Networking Setup
8. Open **Networking** tab and keep all default values:

- Virtual Network → Auto-created  
- Subnet → Auto-created  
- Public IP → Auto-created  

Click **Review + Create**

<img width="1919" height="1079" src="https://github.com/user-attachments/assets/869a2997-6638-45c9-b129-3ffde834a517">

<img width="1919" height="1079" src="https://github.com/user-attachments/assets/dfe1b335-187e-4765-b834-e879aafa1ea1">

---

## 6️⃣ Create the Virtual Machine
9. Click **Create**

<img width="1919" height="1079" src="https://github.com/user-attachments/assets/32e2aca3-900b-4887-add3-9f00b13dd120">

10. Wait **2–3 minutes** for deployment  
11. VM is successfully created 🎉

<img width="1919" height="891" src="https://github.com/user-attachments/assets/f75b0566-7886-4c32-a7d5-9d1ecc249bd8">

---

### ✅ **VM creation completed successfully!**
