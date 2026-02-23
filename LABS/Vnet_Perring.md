# Azure VNet Peering with Two Windows VMs
<img width="944" height="534" alt="Screenshot 2025-11-13 193846" src="https://github.com/user-attachments/assets/c5ea57b4-135a-4741-8dd9-a6a8b743846e" />

---

# 📌 **Step 1 — Create First VNet (10 Network)**

1. Click **Virtual Network**

   ![image](https://github.com/user-attachments/assets/5070d5db-15ac-4b9d-9fdf-136c17482378)

2. Click **Create**

   ![image](https://github.com/user-attachments/assets/3d97f97b-c931-4b5d-bce6-ff7f58014ade)

3. Select Resource Group: `pratham`

4. Type VNet Name: `vnet10`

5. Select Region: `Central India`

6. Go to **IP Addresses** tab

   ![image](https://github.com/user-attachments/assets/250db680-c37f-43a4-9a7e-beec57567ccf)

7. Click **Add Subnet**

8. IP Address Range: `10.0.0.0/16`

9. Subnet Range: `10.0.1.0/24`

10. Click **Add**

11. Click **Review + Create**

![image](https://github.com/user-attachments/assets/58f82d68-e732-48fd-baaa-9cd2be9bc676)

---

# 📌 **Step 2 — Create Second VNet (20 Network)**

1. Click **Virtual Network**

2. Click **Create**

   ![image](https://github.com/user-attachments/assets/3d97f97b-c931-4b5d-bce6-ff7f58014ade)

3. Select Resource Group: `pratham`

4. VNet Name: `vnet20`

5. Region: `Central India`

6. Go to **IP Addresses** tab

   ![image](https://github.com/user-attachments/assets/488459a5-a442-4034-be3e-cd2e0845434e)

7. Click **Add Subnet**

8. IP Range: `20.0.0.0/16`

9. Subnet Range: `20.0.1.0/24`

10. Click **Add**

11. Click **Review + Create**

![image](https://github.com/user-attachments/assets/3a1a60ca-d31f-4788-bea9-a06aa27ed525)

---

# 📌 **Step 3 — Create Windows VM in VNet10**

1. Click **Virtual Machines**

   ![image](https://github.com/user-attachments/assets/692d9f1a-ebd4-4398-990e-fac74ee47045)

2. Click **Create → Virtual Machine**

   ![image](https://github.com/user-attachments/assets/4124bd83-df56-4d1f-a741-13e9c769517b)

3. Resource Group: `pratham`

4. VM Name: `vnet10`

5. Region: `Central India`

6. Availability Zone: `3`

   ![image](https://github.com/user-attachments/assets/d0690df8-aa05-4b59-b94f-0b365f379d7b)

7. Image: Windows Server

8. Select Size

   ![image](https://github.com/user-attachments/assets/fa143b76-a451-4318-825d-491e1616c1d9)

9. Username: `vnet10`

10. Password: ******

11. Inbound Port Rule → Select **RDP (3389)**

12. Click Next: Disk

![image](https://github.com/user-attachments/assets/4c1667d7-431b-4bc7-95c8-b056671ae5a8)

13. Go to **Networking**

![image](https://github.com/user-attachments/assets/ca5fb417-e254-4641-8439-4410a0d36c9b)

14. Select VNet: `vnet10`
15. Click **Review + Create**

![image](https://github.com/user-attachments/assets/040a510e-4e2a-4deb-810e-588056561776)

16. Click **Create**

![image](https://github.com/user-attachments/assets/0fa8fa8c-95e4-420d-bfe8-021a9f3eeb51)

---

# 📌 **Step 3 — Create Windows VM in VNet20 (Same Steps)**

Follow same steps for VM2 with:

* VM Name: `vnet20`
* Username: `vnet20`
* VNet: `vnet20`

Images:

![image](https://github.com/user-attachments/assets/60276263-76aa-452f-89b8-becdbc52be4f)
![image](https://github.com/user-attachments/assets/fa143b76-a451-4318-825d-491e1616c1d9)
![image](https://github.com/user-attachments/assets/064319fc-5cf5-479a-befd-c09d13b6c8aa)
![image](https://github.com/user-attachments/assets/2397dfa8-9fa6-42e4-b2b5-78ac54e6bd3c)
![image](https://github.com/user-attachments/assets/0fa8fa8c-95e4-420d-bfe8-021a9f3eeb51)

---

# 📌 **Step 4 — Create VNet Peering**

1. Click **Virtual Networks**

   ![image](https://github.com/user-attachments/assets/5070d5db-15ac-4b9d-9fdf-136c17482378)

2. Select **vnet10**

   ![image](https://github.com/user-attachments/assets/629eb2e4-056a-4e36-b3ee-eb67e74ade6c)

3. Go to **Settings → Peerings**

   ![image](https://github.com/user-attachments/assets/7545d226-4bea-4608-88dd-ef53ba1c9d29)

4. Click **Add**

   ![image](https://github.com/user-attachments/assets/8b4c2735-dc3a-41f2-aafa-964b41afa874)

5. Peering Name: `VNet10-to-VNet20`

6. Remote VNet: `vnet20`

   ![image](https://github.com/user-attachments/assets/18a3610d-ad14-44bd-8077-cc0f6b5dcc11)

7. Local Peering Name: `VNet20-to-VNet10`

8. Click **Add**

   ![image](https://github.com/user-attachments/assets/1847f1ae-52cd-4681-8488-10e969bb4661)

---

# 📌 **Step 5 — Connect Both VMs using RDP**

1. Click **Virtual Machines**

2. Open VM10

   ![image](https://github.com/user-attachments/assets/275c9d05-39a1-4e00-a7d0-8000c4d5b057)

3. Click **Connect → RDP**

   ![image](https://github.com/user-attachments/assets/afedf0d9-b135-401e-8f56-13476210578b)

4. Copy Public IP

5. Open **Remote Desktop Connection**

   ![image](https://github.com/user-attachments/assets/acdb9bc0-eae4-4c7a-aa7d-d617a08aae5c)

6. Paste Public IP → Connect

   ![image](https://github.com/user-attachments/assets/fcc6906e-7193-44fe-842d-eeed28390217)

7. Enter Username + Password

   ![image](https://github.com/user-attachments/assets/1735008d-12f8-46f6-8cf9-467c52e3a821)

8. Click Yes

   ![image](https://github.com/user-attachments/assets/082bd01f-65ea-4ff1-b9a7-635f9d4af62b)

#### Same steps for VM20.

---

# 📌 **Step 6 — Enable ICMP Ping in Both VMs**

### **On VM10:**

1. Open PowerShell

   ![image](https://github.com/user-attachments/assets/0407b1ee-091d-4bb2-b833-9b85b56d62b8)

2. Check IP

   ```powershell
   ipconfig
   ```

   ![image](https://github.com/user-attachments/assets/90313fe4-51a2-499c-8aa7-5fd52b6a973d)

3. Enable ICMP

   ```powershell
   New-NetFirewallRule -DisplayName "Allow ICMPv4" -Protocol ICMPv4
   ```

   ![image](https://github.com/user-attachments/assets/0f1bf8ef-fca2-49be-be44-6a6adb1f5565)

### **On VM20:**

1. Open PowerShell

2. Run:

   ```powershell
   ipconfig
   ```

   ![image](https://github.com/user-attachments/assets/2dd60770-a01f-4cab-9316-e5b9af8fa72b)

3. Enable ICMP

   ```powershell
   New-NetFirewallRule -DisplayName "Allow ICMPv4" -Protocol ICMPv4
   ```

   ![image](https://github.com/user-attachments/assets/a94fb284-e20e-4202-b533-056fc7d2d5e9)

---

# 📌 **Step 7 — Ping Test**

From VM10 → Ping VM20 private IP

```cmd
ping 20.0.2.4
```

![image](https://github.com/user-attachments/assets/a7487c71-183e-4e9e-8bf1-0eaad0546b2d)

---

# ✅ **VNet Peering Successfully Completed!**
