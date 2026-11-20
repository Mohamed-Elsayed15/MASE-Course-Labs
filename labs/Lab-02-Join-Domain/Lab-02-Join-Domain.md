# Lab 02: Joining a Client Machine to a Windows Server Domain

## 📋 Lab Overview
This lab demonstrates the step-by-step process of joining a Windows 10 client machine (`HR-pc01`) to an Active Directory Domain (`test.local`) hosted on Windows Server 2019, including diagnosing and resolving a DNS lookup timeout issue (`ERROR_TIMEOUT`).

---

## 🛠️ Lab Environment
- **Domain Controller:** Windows Server 2019 (`test.local` — IP: `192.168.1.2`)
- **Client Machine:** Windows 10 (`HR-pc01` — IP: `192.168.1.20`)

---

## 🚀 Step-by-Step Execution

### 1. Client Preparation (IP & DNS Configuration)
Before attempting to join the domain, the client machine was prepared by synchronizing date/time, renaming the PC to `HR-pc01`, and configuring a static IP address pointing to the Domain Controller as its Preferred DNS Server (`192.168.1.2`).

![IP and DNS Configuration](images/4.png)

---

### 2. Attempting to Join the Domain
Navigated to **System Properties** > **Computer Name** > **Change**, switched membership from `WORKGROUP` to `Domain`, and entered `test.local`.

![Domain Join Attempt](images/1.png)

---

### 3. Troubleshooting: Active Directory Domain Controller Error
Upon attempting to join, Windows returned the following error:
> *"An Active Directory Domain Controller (AD DC) for the domain 'test.local' could not be contacted."*

![AD DC Contact Error](images/2.png)

#### Diagnosis & Resolution
1. **Network Connectivity Check:** Ran `ping 192.168.1.2` from Command Prompt, confirming 0% packet loss and healthy Layer 3 connectivity to the server.
2. **Root Cause Analysis:** Checked the error details (`0x000005B4 ERROR_TIMEOUT`), which pointed to a DNS SRV record query failure. After correcting the DNS configuration, the client successfully resolved `test.local`.

![Ping Test and Error Details](images/3.jpg)

---

### 4. Authentication & Domain Join Confirmation
Once DNS resolution succeeded, a prompt appeared requesting administrative credentials authorized to join machines to the domain.

![Domain Credentials Prompt](images/5.png)

After entering the IT Admin credentials, the join completed with the official welcome message:

![Welcome to Domain](images/6.png)

---

### 5. Verification on Server & Client Login
1. **Active Directory Verification:** Opened **Active Directory Users and Computers** on Windows Server 2019 and confirmed that `HR-PC01` appeared under the `Computers` container.

![AD Verification](images/7.png)

2. **Client Restart & Login:** Rebooted the client machine and signed in to the domain successfully.

![Client Login Screen](images/8.png)
