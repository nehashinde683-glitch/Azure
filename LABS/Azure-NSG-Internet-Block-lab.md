# 🔐 Azure NSG Internet Block Lab 
This lab demonstrates how to:

- ✔ Create a Virtual Network  
- ✔ Create a Windows Server VM (No Public IP)  
- ✔ Create an NSG rule to block all outbound internet traffic  
- ✔ Access VM securely using Azure Bastion  
- ✔ Verify that the internet is blocked  

All steps include screenshots for better understanding.

---

# 🧩 Architecture Diagram
<img width="1660" height="472" alt="image" src="https://github.com/user-attachments/assets/931267ec-5e93-43d9-945a-1283a9a152c7" />

---

# 🟦 Step 1 — Create Virtual Network for Bastion

1. Click **Virtual Network**  
   ![](https://github.com/user-attachments/assets/9acbf209-4afd-4170-910a-63c82d3256e0)

2. Click **Create**  
   ![](https://github.com/user-attachments/assets/bdfa34e6-7c5c-497b-89ea-69a505b49973)

3. Resource Group: `Pratham`

4. VNet Name: **Vnet**

5. Region: **Central India**

6. Click **IP Addresses** tab  
   ![](https://github.com/user-attachments/assets/8926d4b1-be86-4243-bfd5-feb4089227f7)

7. Keep the default subnet as it is.

8. Click **Add Subnet**

9. Subnet Purpose: **Azure Bastion**

10. Address Range: `10.0.1.0/24`

11. Click **Save**

12. Click **Review + Create**  
   ![](https://github.com/user-attachments/assets/75498202-422a-45bb-82e4-088d084c0f5d)

13. Click **Create**  
   ![](https://github.com/user-attachments/assets/a54eef3f-8c96-4008-84db-865c3628d348)

---

# 🟩 Step 2 — Create Windows VM (Without Public IP)

1. Click **Virtual Machines**  
   ![](https://github.com/user-attachments/assets/f3f5d080-900d-4233-9a98-ed798b41fe8c)

2. Click **Create → Virtual Machine**  
   ![](https://github.com/user-attachments/assets/37cc27f8-d7af-4813-bc19-04d06f5373b9)

3. Resource Group: `Pratham`

4. VM Name: **VM**

5. Region: **Central India**  
   ![](https://github.com/user-attachments/assets/474d0884-1fc0-404d-8953-67bd300df8c8)

6. Image: **Windows Server**

7. Choose VM Size  
   ![](https://github.com/user-attachments/assets/ac75eb19-3c9f-4980-a41d-a74c97bb389f)

8. Username: `VM`  
9. Password: `********`

10. Enable inbound port: **RDP (3389)**

11. Click **Next: Disk**  
   ![](https://github.com/user-attachments/assets/2a83f5a9-4e1c-4dde-92f9-c38b1e11a0b7)

12. Go to **Networking**

13. Select VNet → **Vnet**

14. Select Subnet → **Default**

15. Public IP: **None**

16. Click **Review + Create**  
    ![](https://github.com/user-attachments/assets/c66d4e85-a237-4729-bd38-5ae2f278752c)

17. Click **Create**  
    ![](https://github.com/user-attachments/assets/55b62440-f4f5-41bd-bbac-37c9f62f1bf4)

---

# 🟥 Step 3 — Create NSG (Internet BLOCK RULE)

1. Click **Virtual Machines**  
   ![](https://github.com/user-attachments/assets/f3f5d080-900d-4233-9a98-ed798b41fe8c)

2. Select your VM  
   ![](https://github.com/user-attachments/assets/7adf5c07-f819-430f-a795-0a5aa5aaaf23)

3. Click **Networking**

4. Click **Create Port Rule**

5. Select **Outbound Port Rule**  
   ![](https://github.com/user-attachments/assets/ceb80f2f-cfb6-4000-8912-206e669680c2)

6. Add Outbound Security Rule  

| Setting | Value |
|--------|--------|
| Source | Any |
| Source Port Range | * |
| Destination | Any |
| Service | Custom |
| Destination Port Range | * |
| Protocol | Any |
| Action | Deny |
| Priority | 100 |
| Name | Deny-Internet |

7. Click **Add**  
   ![](https://github.com/user-attachments/assets/69082e3e-b6e6-4298-8c2c-47f2e7727f78)  
   ![](https://github.com/user-attachments/assets/6260dd8c-13e9-46a7-949c-8ab6325e4b1d)

---

# 🟦 Step 4 — Connect to VM Using Bastion

1. Click **Virtual Machines**  
2. Select VM  
3. Click **Connect → Bastion**  
   ![](https://github.com/user-attachments/assets/a006d4f5-d217-4501-b902-19b7b16f4a50)

4. Enter:
- Username: `vm`  
- Password: `********`

5. Click **Connect**

6. VM Login Successful  
   ![](https://github.com/user-attachments/assets/f8a71bf1-d7eb-4f68-9ee1-1e7ed2935b77)

---

# 🟩 Step 5 — Verify Internet Is Blocked

1. Open **Microsoft Edge**  
   ![](https://github.com/user-attachments/assets/190c063a-ffdb-4fe4-a957-07ae82a51763)

2. Search any website → **It will NOT open**  
   ![](https://github.com/user-attachments/assets/2f606655-67d0-4ea7-b3a8-a419635a4193)

---

# 🎉 FINAL RESULT

- NSG Outbound rule applied successfully  
- Internet access is fully blocked  
- VM accessible only via Azure Bastion  
- Secure isolation of workloads  

---

# 👑 Author  
**Pratham**
