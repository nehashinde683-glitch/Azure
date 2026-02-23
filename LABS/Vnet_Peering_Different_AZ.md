# Azure VNet Peering Between Different Regions (Central India ↔ East Asia)

This README.md provides **step-by-step documentation** with **all images**, covering:

* Two VNets in different regions
* Two Windows VMs
* VNet Peering across regions
* RDP access
* Enabling ICMP (private & public IP)
* Ping test

---

# 🚀 **STEP 1 — Create VNet1 (Central India)**

1. Click **Virtual Network**
   ![](https://github.com/user-attachments/assets/2cc987c7-e66b-4248-b097-698dbcd1b1b8)

2. Click **Create**
   ![](https://github.com/user-attachments/assets/b5540a1c-667d-40a2-8b2b-4dcd1c7fa12a)

3. Select Resource Group: `pratham`

4. VNet Name: **VNET10**

5. Region: **Central India**

6. Go to **IP Addresses** tab
   ![](https://github.com/user-attachments/assets/be42924d-32b9-434e-8038-fef3724f2af7)

7. Click **Add Subnet**

8. IP Range: `10.0.0.0/16`

9. Subnet Range: `10.0.1.0/24`

10. Click **Add**

11. Click **Review + Create**
    ![](https://github.com/user-attachments/assets/58f82d68-e732-48fd-baaa-9cd2be9bc676)

---

# 🌍 **STEP 2 — Create VNet2 (East Asia)**

1. Click **Virtual Network → Create**
   ![](https://github.com/user-attachments/assets/933564a6-82b9-427c-b157-f8d046438939)

2. Resource Group: `pratham`

3. VNet Name: **VNET20**

4. Region: **East Asia**

5. Go to **IP Addresses** tab
   ![](https://github.com/user-attachments/assets/00af027e-9ccb-454f-a220-588ecd4b01bb)

6. Click **Add Subnet**

7. IP Range: `20.0.0.0/16`

8. Subnet Range: `20.0.1.0/24`

9. Click **Add**

10. Click **Review + Create**
    ![](https://github.com/user-attachments/assets/65825cd1-0387-4589-a39b-0ddc7b555249)

---

# 💻 **STEP 3 — Create Windows VM1 in VNET10**

1. Click **Virtual Machines**
   ![](https://github.com/user-attachments/assets/692d9f1a-ebd4-4398-990e-fac74ee47045)

2. Click **Create → Virtual Machine**
   ![](https://github.com/user-attachments/assets/4124bd83-df56-4d1f-a741-13e9c769517b)

3. Resource Group: `pratham`

4. VM Name: **VNET10**

5. Region: **Central India**

6. Availability Zone: **3**
   ![](https://github.com/user-attachments/assets/5af6ce9f-20cc-42cc-bdbc-322255e0e36c)

7. Image: **Windows Server**

8. Select Size
   ![](https://github.com/user-attachments/assets/a6549bcc-752c-484e-a133-59914e07a64a)

9. Username: `VNET10`

10. Password: ******

11. Enable **RDP (3389)**

12. Disk → Next
    ![](https://github.com/user-attachments/assets/dacd2d7c-117a-4615-a94f-779857a53f23)

13. Networking → Select VNet: **VNET10**
    ![](https://github.com/user-attachments/assets/ca5fb417-e254-4641-8439-4410a0d36c9b)

14. Review + Create
    ![](https://github.com/user-attachments/assets/0a66fadb-bac9-44b3-a6bb-0e5ed6c1570b)

15. Click **Create**
    ![](https://github.com/user-attachments/assets/24bf946e-907b-4c6b-9d0e-caf03c5cf403)

---

# 💻 **STEP 3 — Create Windows VM2 in VNET20**

Follow the same steps as VM1 with:

* VM Name: **VNET20**
* Region: **East Asia**
* Username: `VNET20`

Images:
![](https://github.com/user-attachments/assets/d44ee747-44d6-4f36-b811-98d5df576d19)
![](https://github.com/user-attachments/assets/073cc8dc-cef2-40eb-85fc-af1c995777aa)
![](https://github.com/user-attachments/assets/dd389fde-5043-438a-8ee9-d95712a9bcc9)
![](https://github.com/user-attachments/assets/b9f0bd77-7f73-49e3-b9c9-e9511cc5db4f)
![](https://github.com/user-attachments/assets/24bf946e-907b-4c6b-9d0e-caf03c5cf403)

---

# 🔗 **STEP 4 — Create VNet Peering (Cross-Region)**

1. Click **Virtual Networks**

2. Select **VNET10**
   ![](https://github.com/user-attachments/assets/4b6d0587-b4ef-4099-86f7-baa061b4ab08)

3. Go to **Peerings**
   ![](https://github.com/user-attachments/assets/27429735-f046-453d-85fb-1ec7ab7a2447)

4. Click **Add**
   ![](https://github.com/user-attachments/assets/8b4c2735-dc3a-41f2-aafa-964b41afa874)

5. Peering Name: `VNET10-TO-VNET20`

6. Remote VNet: **VNET20**
   ![](https://github.com/user-attachments/assets/ffe4bfc5-04b6-4ea6-b3fd-c874d56e593e)

7. Local Peering Name: `VNET20-TO-VNET10`

8. Click **Add**
   ![](https://github.com/user-attachments/assets/4731982b-8ddf-4ff3-86a3-87ffeacbf447)

---

# 🖥️ **STEP 5 — Connect to Both VMs using RDP**

### Connect VNET10 VM

![](https://github.com/user-attachments/assets/74d3415a-1a51-46de-a417-0c0b0419a394)
![](https://github.com/user-attachments/assets/4be3b313-670f-4ae6-8075-1711b20b871c)
![](https://github.com/user-attachments/assets/bb5fb724-3d6b-4cee-9d20-ace27742d6ae)
![](https://github.com/user-attachments/assets/742d5ba5-f364-4abd-8cbb-8cc990b79fdb)

## Same steps for **VNET20**.

---

# 🔥 **STEP 6 — Enable ICMP (Private Ping) inside Both VMs**

1. Open **Server Manager**
   ![](https://github.com/user-attachments/assets/f683bc0e-e2c8-4504-a0a1-ac9dfe43ad21)

2. Tools → **Windows Defender Firewall with Advanced Security**
   ![](https://github.com/user-attachments/assets/342127fc-2f7f-48b0-9d72-f008e7da6a02)

3. Inbound Rules → **New Rule**
   ![](https://github.com/user-attachments/assets/1f497e07-4a84-4699-b9c2-edfc9737b9b9)

4. Choose **Custom → Next**

5. Protocol Type: **ICMPv4**
   ![](https://github.com/user-attachments/assets/b6c431a1-e58e-4bbf-89a0-b4e2daa1c918)

6. Name: `ICMP`

7. Finish
   ![](https://github.com/user-attachments/assets/0de194d8-e709-4f70-9c6a-06e6a9970da7)

---

# 🌐 **STEP 6 — Enable ICMP for Public Ping (NSG Rule)**

1. Open VM → **Networking**
2. Create inbound rule:

   * Protocol: **ICMP**
   * Action: **Allow**
     ![](https://github.com/user-attachments/assets/58bab089-82b9-4be2-bc1e-f6f3533503e7)
     ![](https://github.com/user-attachments/assets/995de4fd-3e6e-4481-a30e-de7b724693e3)

## Same for **VNET20**.

---

# 🧪 **STEP 7 — Ping Test**

### 🔹 Private Ping (VM20 → VM10)

```
ping 10.0.2.4
```

![](https://github.com/user-attachments/assets/ccb7d694-be57-421b-aef2-2fe6ecd5c9d6)

---

### 🔹 Public Ping

```
ping 4.240.83.202
```

![](https://github.com/user-attachments/assets/d48f6860-9238-47ba-a889-eb43f463b7a8)

---

# 🎉 **VNet Peering Across Regions Successfully Completed!**
