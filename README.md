### **Complete Detailed Notes: IT System Engineer & Cloud Administration**  
*(All topics covered systematically with examples)*  

---

#### **1. Active Directory (AD) & AD Domain Services (ADDS)**  
**What it is**:  
Centralized database for managing **users, computers, printers, and security policies** in a Windows network.  
**Key Components**:  
- **Domain Controller (DC)**: Server hosting ADDS (handles logins, authentication).  
- **Organizational Unit (OU)**: Container for grouping objects (e.g., "Finance OU" for accountants).  
- **Forest**: Collection of multiple domains sharing trust (e.g., `corp.com` + `asia.corp.com`).  
- **Schema**: Rules defining object types (users, groups) and attributes.  
**Real-World Example**:  
When you log into a work laptop, the DC verifies your credentials and grants access to shared drives.  

---

#### **2. DNS Zones**  
**What it is**:  
Segments of DNS namespace managed by a server. Translates domain names → IP addresses.  
**Types**:  
- **Primary Zone**: Read/write copy (editable).  
- **Secondary Zone**: Read-only replica (for redundancy).  
- **Stub Zone**: Only stores names of authoritative servers.  
**Example**:  
`printer1.office.local` → `192.168.1.50` (Forward Lookup).  
**Real-World Use**:  
Websites like `google.com` rely on DNS to resolve to IPs like `142.250.189.206`.  

---

#### **3. Group Policy**  
**What it is**:  
Tool to enforce settings across users/computers in AD.  
**Key Concepts**:  
- **GPO (Group Policy Object)**: Container for settings (e.g., "Disable USB ports").  
- **Processing Order**: Local → Site → Domain → OU (child OUs override parents).  
- **Enforced/Block Inheritance**: Force policies or block higher-level GPOs.  
**Real-World Example**:  
A hospital forces screen locks after 5 minutes on all clinical workstations via GPO.  

---

#### **4. BitLocker Encryption**  
**What it is**:  
Full-disk encryption for Windows devices (laptops/servers).  
**How it Works**:  
- Uses **TPM chip** to store keys.  
- **Recovery Key**: Backup to AD or file.  
**Real-World Use**:  
A stolen company laptop with BitLocker remains secure; data inaccessible without PIN/recovery key.  

---

#### **5. Windows Server 2022**  
**What it is**:  
Microsoft’s server OS for hosting services (AD, DNS, file sharing).  
**Key Roles**:  
- **Domain Controller**: Runs ADDS.  
- **DHCP Server**: Assigns IP addresses automatically.  
- **Hyper-V**: Virtualization platform.  
**Example**:  
A school uses Windows Server 2022 as a DC + file server for student documents.  

---

#### **6. Azure Active Directory (Azure AD)**  
**What it is**:  
Cloud identity service for **managing users/app access** (different from on-prem AD).  
**Key Features**:  
- **SSO (Single Sign-On)**: One login for Microsoft 365, Salesforce, etc.  
- **MFA (Multi-Factor Authentication)**: Extra login security (e.g., phone app code).  
- **Conditional Access**: Block logins from risky locations.  
**Real-World Example**:  
Employees sign into Outlook/Teams with Azure AD credentials.  

---

#### **7. Microsoft 365**  
**What it is**:  
Subscription suite including **Office apps + cloud services**.  
**Core Services**:  
- **Exchange Online**: Cloud email (Outlook).  
- **SharePoint Online**: Document collaboration.  
- **Teams**: Meetings/chat.  
**Real-World Use**:  
Remote teams co-edit PowerPoint files in SharePoint and meet via Teams.  

---

#### **8. Microsoft Groups (M365 Groups)**  
**What it is**:  
Shared workspace combining **Outlook inbox, SharePoint, Planner, and Teams**.  
**How it Works**:  
Create "Project Alpha Group" → Auto-generates:  
- Shared email (`project-alpha@company.com`)  
- SharePoint site for files  
- Teams channel  
**Example**:  
Marketing team shares campaign assets in one Group without manual setup.  

---

#### **9. Microsoft Intune**  
**What it is**:  
Cloud service for **managing devices/apps** (mobile/desktop).  
**Key Tasks**:  
- **Device Enrollment**: Register company phones/laptops.  
- **Compliance Policies**: "Require Android devices to encrypt storage."  
- **App Protection**: Prevent copying data from company apps to personal apps.  
**Real-World Use**:  
IT remotely wipes company data from a lost employee iPhone via Intune.  

---

#### **10. Azure AD Connect**  
**What it is**:  
Tool to **sync on-prem AD users → Azure AD** (hybrid identity).  
**Sync Options**:  
- **Password Hash Sync**: On-prem passwords synced to cloud.  
- **Pass-Through Authentication (PTA)**: Cloud logins validated by on-prem DC.  
**Real-World Example**:  
Employees use the same password for on-prem PCs (AD) and Microsoft 365 (Azure AD).  

---

#### **11. Azure Virtual Machines (VMs)**  
**What it is**:  
Cloud-based Windows/Linux servers.  
**Key Features**:  
- **Images**: Preconfigured templates (Windows Server, Ubuntu).  
- **Scaling**: Resize CPU/RAM on demand.  
- **Disks**: SSD/HDD storage.  
**Example**:  
Hosting a customer database on an Azure VM instead of physical hardware.  

---

#### **12. Azure Networking**  
**Core Services**:  
- **Virtual Network (VNet)**: Private cloud network (e.g., `10.1.0.0/16`).  
- **VPN Gateway**: Connect on-prem network → Azure VNet.  
- **Load Balancer**: Distribute traffic across VMs.  
**Real-World Use**:  
E-commerce app uses Load Balancer to handle traffic spikes during sales.  

---

#### **13. Azure Storage**  
**Types**:  
- **Blob Storage**: Unstructured data (images/videos).  
- **File Shares**: SMB-based cloud file shares (like on-prem network drives).  
- **Disk Storage**: VM hard drives.  
**Example**:  
A mobile app stores user profile pictures in Blob Storage.  

---

#### **14. Azure Backup**  
**What it is**:  
Automated backup for **VMs, files, databases**.  
**Key Features**:  
- **Retention Policies**: Keep backups for 99 years.  
- **Application-Consistent Backups**: Safe backups for SQL/Exchange.  
**Real-World Use**:  
Restore a corrupted Azure VM from yesterday’s backup in 15 minutes.  

---

#### **15. Azure Key Vault**  
**What it is**:  
Secure storage for **passwords, API keys, SSL certificates**.  
**Key Uses**:  
- Store database connection strings.  
- Rotate encryption keys automatically.  
**Example**:  
A weather app retrieves its API key from Key Vault instead of hardcoding it.  

---

### **Deep Dives & Diagrams**  

#### **ADDS Architecture**  
```  
Forest (root)  
└─ Domain (corp.com)  
   ├─ OU: Finance  
   │  ├─ User: Alice  
   │  └─ Computer: Finance-PC1  
   └─ OU: IT  
      ├─ User: Bob  
      └─ Group: Admins  
```  
**Global Catalog**: Partial replica of all domains in a forest for fast searches.  

---

#### **Azure AD Connect Sync Flow**  
```  
On-Prem AD → Azure AD Connect → Azure AD  
      (Syncs users/groups)  
```  
**Filtering**: Sync only users in "Sales" OU.  

---

#### **Intune Device Management**  
```  
Devices (iOS/Android/Windows)  
↓  
Intune Cloud (Apply policies: "Require PIN")  
↓  
Admin Portal (Wipe lost device)  
```  

---

### **Practice Questions**  
1. **Group Policy**:  
   *A GPO enforcing "Disable USB Storage" is linked to the "Engineering" OU. A conflicting GPO allowing USB storage is linked to the domain. Which applies to Engineering users?*  
   **Answer**: "Disable USB Storage" (OU GPOs override domain).  

2. **Azure Networking**:  
   *Can two VMs in different subnets (10.1.1.0/24 and 10.1.2.0/24) communicate?*  
   **Answer**: Yes (default routing within a VNet).  

3. **BitLocker**:  
   *Where is the recovery key stored if integrated with AD?*  
   **Answer**: In the Active Directory object of the encrypted device.  

---

### **Study Priority & Tips**  
1. **Start On-Prem**:  
   AD → DNS → Group Policy → Windows Server → BitLocker.  
2. **Cloud Identity**:  
   Azure AD → Microsoft 365 → Intune → Azure AD Connect.  
3. **Azure Infrastructure**:  
   Azure VMs → Networking → Storage → Backup → Key Vault.  
**Hands-On Labs**: Use [Azure Free Tier](https://azure.microsoft.com/free/) to deploy VMs/storage.  

Let me know if you need flashcards, more questions, or Azure CLI commands!
