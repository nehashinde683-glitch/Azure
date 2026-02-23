# 🔥 Azure Firewall + Windows VM + DNAT (RDP) Full Setup Guide  
This documentation explains how to create:

- ✔ 1 VNet  
- ✔ Subnet for VM  
- ✔ Subnet for Azure Firewall  
- ✔ Windows Server VM  
- ✔ Azure Firewall (Standard)  
- ✔ DNAT Rule to allow RDP using Firewall Public IP  

All steps include screenshots for better understanding.

---

# 🧩 Architecture Diagram

<img width="1252" height="716" alt="image" src="https://github.com/user-attachments/assets/5f16b01e-69ff-4030-b6ee-bf405d715ea2" />

---
# 🚀 STEP 1 — Create Virtual Network (VNet)

### 1. Open **Virtual Network**
![](https://github.com/user-attachments/assets/2cc987c7-e66b-4248-b097-698dbcd1b1b8)

### 2. Click **Create**
![](https://github.com/user-attachments/assets/b5540a1c-667d-40a2-8b2b-4dcd1c7fa12a)

### 3. Fill Basic Details
- **Resource Group:** `pratham`  
- **VNet Name:** `VNET`  
- **Region:** `Central India`

### 4. Go to **IP Addresses** tab  
![](https://github.com/user-attachments/assets/591b61d7-7d1f-4aeb-bfcf-0a7c0d1d2be4)

---

## ➤ Create Subnet1 (For VM)

### 5. Click **Add Subnet**
### 6. Click edit ✏️ icon  
### 7. Enter details:
- **Subnet Name:** `SUBNET1`
- **VNet Range:** `10.0.0.0/16`
- **Subnet Range:** `10.0.1.0/24`

![](https://github.com/user-attachments/assets/7cfd3e86-82af-4850-92e5-97cf242380ea)

---

## ➤ Create Azure Firewall Subnet

### 8. Click **Add Subnet**
- **Subnet Purpose:** `Azure Firewall`
- **Name:** `AzureFirewallSubnet`
- **VNet Range:** `10.0.0.0/16`
- **Subnet Range:** `10.0.2.0/24`

![](https://github.com/user-attachments/assets/c4e0d770-b1ae-4918-9549-71c689511059)

### 9. Click **Review + Create**  
### 10. Click **Create**  

![](https://github.com/user-attachments/assets/7d424c66-3279-4bf3-b98b-2020625e1ffa)

---

# 💻 STEP 2 — Create Windows Server VM

### 1. Click **Virtual Machines**
![](https://github.com/user-attachments/assets/692d9f1a-ebd4-4398-990e-fac74ee47045)

### 2. Click **Create → Virtual Machine**
![](https://github.com/user-attachments/assets/4124bd83-df56-4d1f-a741-13e9c769517b)

### 3. Fill Basic Details
- **Resource Group:** `pratham`
- **VM Name:** `VM`
- **Region:** `Central India`
- **Availability Zone:** 3  
![](https://github.com/user-attachments/assets/ff25d1ae-4543-48f2-a766-91e25a16c7e0)

### 4. Select Image & Size
![](https://github.com/user-attachments/assets/eeaa1131-8132-493a-b8bd-58d6679396bc)

### 5. Provide Credentials
- Username: `VM`
- Password: `*******`

### 6. Enable **RDP (3389)**  
### 7. Click **Next: Disk**  
![](https://github.com/user-attachments/assets/8e37feff-a0da-4904-9b8a-8ebd80ddf378)

### 8. Networking
- Select VNet → `VNET`
- Select Subnet → `SUBNET1`

![](https://github.com/user-attachments/assets/540bc0c0-0852-4eb3-a184-6b4375c2297a)

### 9. Click **Review + Create** → **Create**  
![](https://github.com/user-attachments/assets/b15c5f29-c5ef-45f7-b0ec-f01ef85e128f)

---

# 🔥 STEP 3 — Create Azure Firewall

### 1. Search **Firewall**
![](https://github.com/user-attachments/assets/7e837283-14bc-4d87-bb21-c580b0f1d318)

### 2. Click **Create**
![](https://github.com/user-attachments/assets/1f6ce662-20a5-4fb6-a80a-dcb6f1051f7f)

### 3. Fill Details
- **Resource Group:** `pratham`
- **Name:** `FIREWALL`
- **Region:** `Central India`
- **SKU:** `Standard`

![](https://github.com/user-attachments/assets/fb03804a-987a-4c0c-8e52-bbe8f19cb1bb)

### 4. Configuration
- Firewall management → **Use firewall rules (classic)**
- Virtual network → **Use existing**
- Select VNet → `VNET`
- Create Public IP → `FIREWALL-IP-PUB`

![](https://github.com/user-attachments/assets/eb37ca82-2167-436b-8049-ca8561aeae3e)

### 5. Disable Firewall Management NIC  
![](https://github.com/user-attachments/assets/fae1e142-148f-4bc5-9ff1-7f02c7c458f9)

### 6. Click Review + Create → Create  
![](https://github.com/user-attachments/assets/989a68ff-2e9c-4e98-b323-c5b2381860a9)

---

# 🔥 STEP 4 — Add DNAT Rule for RDP

### 1. Go to Firewall → **Rules (Classic)** 

### 2. Click **Add NAT Rule Collection**
![](https://github.com/user-attachments/assets/a96e4b8e-c639-4d4d-bf89-1557717ed8b7)

### 3. Enter Rule Details  
| Field | Value | Explanation |
|-------|--------|-------------|
| Name | DNAT | DNAT = Destination NAT (Firewall Public IP → VM Private IP mapping) |
| Priority | Your choice | Lower number = Higher priority. Example: 100, 200, 300 |
| Rule Name | RDP | Rule for allowing RDP traffic |
| Protocol | TCP | RDP works securely on **TCP protocol** (UDP optional nahi chahiye) |
| Source Type | * (ANY) | `*` **means ANY IP address** → any public IP can try to access RDP (production me restrict karna recommended) |
| Destination Address | Firewall Public IP | Because RDP request first hits the Firewall, not the VM |
| Destination Port | 3389 | **3389 = Default RDP port** used for Remote Desktop |
| Translated Address | VM Private IP | Firewall will forward traffic from public → internal VM |
| Translated Port | 3389 | RDP uses same port internally as well |


![](https://github.com/user-attachments/assets/eb4e278e-368d-40f1-899d-c4b55c7269cd)

---

# 🟢 STEP 5 — Connect via RDP

### 1. Open Remote Desktop  
![](https://github.com/user-attachments/assets/e57bc33b-a42b-4321-95e9-2f625e00e74a)

### 2. Enter **Firewall Public IP**
![](https://github.com/user-attachments/assets/704fee5d-16ed-4413-b807-211a1d3eac63)

### 3. Enter VM Credentials  
![](https://github.com/user-attachments/assets/07b1262d-3cd2-4b1c-8e0f-52daacdacf59)

### 4. SUCCESS — VM Connected via Firewall 🔥  
![](https://github.com/user-attachments/assets/a8541fbb-cfc5-404f-a17b-ad12530f02d9)

---

# 🎉 FINAL RESULT
- Azure Firewall working  
- Windows VM successfully RDP via Firewall  
- Secure DNAT rule created  
- Working architecture with screenshots  

---

# 👑 Author  
**Pratham**
