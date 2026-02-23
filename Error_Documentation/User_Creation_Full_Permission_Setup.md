# 🧑‍💻 Azure User Creation and Full Permission Setup


## 📘 Step 1: Create a New User

### 1. Open the Azure Portal
- Navigate to: [https://portal.azure.com](https://portal.azure.com)

### 2. Go to "Users" Section
- From the **left-hand menu**, click on **Users**.

![Click on User](https://github.com/user-attachments/assets/01067bf6-55bc-45d2-b74b-39ae81019d22)

---

### 3. Click on **New User**
![Click on New User](https://github.com/user-attachments/assets/1715d5fa-c0ba-4620-b9c5-26b7a7c8b298)

---

### 4. Click on **Create New User**
![Create New User](https://github.com/user-attachments/assets/7ffc5dc4-e082-464f-9ca0-2c6bdb6ee9c8)

---

### 5. Enter User Details

| Field | Value |
|--------|--------|
| **User Principal Name** | `Kunal` |
| **Display Name** | `Kunal` |
| **Password** | `Pote@123` |

---

### 6. Click **Next: Properties**
![Next Properties](https://github.com/user-attachments/assets/59b2b5b6-340f-41b1-b0e7-be1ccfc599f9)

---

### 7. Click on **Assignments**
![Assignments](https://github.com/user-attachments/assets/0d84a920-6f1b-4292-8005-16fee8d80aa4)

---

### 8. Click on **Add Role**

- In the **Search box**, type **Global**  
- Select **Global Administrator**  
- Click on **Select**

![Select Global Administrator](https://github.com/user-attachments/assets/fd90071a-4d63-4d45-bacf-ed3faf9f0646)

---

### 9. Click **Review + Create**
- Then click **Create** to finalize the new user.

![Click Create](https://github.com/user-attachments/assets/8355e76e-3554-44be-81bb-205552c419c3)

---

## 🛠️ Step 2: Give Full Permission to the User

### 1. Search for **Subscriptions**
- In the Azure search bar, type **Subscription**.

### 2. Click on **Subscription**
![Click on Subscription](https://github.com/user-attachments/assets/48929d17-b677-4025-bda4-56ca043303cd)

---

### 3. Select Your Active Subscription
- Click on **Azure Subscription 1**

![Azure Subscription 1](https://github.com/user-attachments/assets/a6739be0-fb43-4741-b1f6-90d889199303)

---

### 4. Open **Access Control (IAM)**

### 5. Click **Add → Add Role Assignment**
![Add Role Assignment](https://github.com/user-attachments/assets/da77b7e1-9927-4549-bb5c-8eb843efc341)

---

### 6. Select a Privileged Administrator Role
- Choose **Owner** or **Contributor**

![Choose Role](https://github.com/user-attachments/assets/aa4f7f49-572c-42a0-9d3a-c330baa885f5)

---

### 7. Assign to the User
- Click **Select Members**
- Choose **Kunal**
- Click **Select**

![Select Member](https://github.com/user-attachments/assets/a0a51b9e-295b-469f-9ee9-f70ae08829a7)

---

### 8. Click **Review + Create**
- Confirm all settings and click **Create**.

![Review and Create](https://github.com/user-attachments/assets/898c6c87-513b-4e94-b8c0-0c380a77f811)

---

## ✅ Step 3: Verify the User Account

### 1. Go to Microsoft Azure Portal
- Visit: [https://portal.azure.com](https://portal.azure.com)

### 2. Log in with the New User Credentials

| Field | Value |
|--------|--------|
| **Email ID** | `Kunal@prathamkukudkargmail.onmicrosoft.com` |
| **Password** | `Pote@123` |

---

### 3. Set a New Password
- After first login, Azure will prompt you to change the password.

![Set New Password](https://github.com/user-attachments/assets/528daf3e-aa5e-4ba3-a0e1-685a3a041248)

---

### 4. Configure Multi-Factor Authentication (MFA)
- Download the **Microsoft Authenticator App**.
- Scan the **QR code** shown on screen.

---

### 5. Access Azure Dashboard
- After successful verification, you can now see the **Azure Dashboard** as the new user.

![Azure Dashboard](https://github.com/user-attachments/assets/173c195e-4521-402e-8649-7c45161ad04f)

---

