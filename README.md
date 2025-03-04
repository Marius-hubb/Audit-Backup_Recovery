# 🔒 Auditing Data Backup & Recovery in Windows

## **📚 Lab Overview**
This lab demonstrates how to audit **data backup and recovery** in a Windows environment, ensuring compliance with **ISO 27001, PCI DSS, NIST 800-53, and HIPAA**. The focus is on **policy enforcement, log verification, access control, and security monitoring**.

## **🔍 Lab Objectives**
- Verify and document **backup policies, permissions, and security controls**.
- Assess compliance with **data retention and recovery standards**.
- Audit **backup encryption, access control, and restoration effectiveness**.
- Identify **gaps in business continuity planning (BCP) and disaster recovery (DR)**.

---

## **💻 Lab Tasks**

### **✅ Step 1: Verify Backup Policies & Configuration**
1. **Check Backup Policies in Group Policy**
   - Open **Group Policy Management Console (GPMC)** (`gpedit.msc`).
   - Navigate to:
     ```
     Computer Configuration > Administrative Templates > Windows Components > Backup
     ```
   - Verify whether **backup policies are enabled** and aligned with security policies.
   - Document policy settings and compliance gaps.

2. **Check Backup Storage Location & Access Permissions**
   - Open **File Explorer** and navigate to the backup folder (`C:\Data Backup`).
   - Right-click **Properties** > **Security Tab** > **Advanced**.
   - Verify **who has access** and document any **excessive permissions**.
   - Run PowerShell to list folder permissions:
     ```powershell
     Get-Acl "C:\Data Backup" | Format-List
     ```
   - If **"Everyone"** has Full Control ➔ **Report a security risk**.

---

### **✅ Step 2: Perform & Audit a Windows Server Backup**
1. **Launch Windows Server Backup (`wbadmin.msc`)**
   - Navigate to **Local Backup** > **Backup Once**.
   - Select **Custom Backup** and add the folder (`C:\Internal Files`).
   - Choose **Remote Shared Folder** (`\\DOMAINCONTROLL\Data Backup`).
   - **Audit Log:** Record the date, backup location, and completion status.

2. **Verify Backup Completion & Audit Logs**
   - Open **Event Viewer (`eventvwr.msc`)**.
   - Go to **Applications and Services Logs > Microsoft > Windows > Backup**.
   - **Check for Event ID 4 (Backup Successful)** or **Event ID 49 (Backup Failure)**.
   - **Document findings** in an audit report.

---

### **✅ Step 3: Simulate Data Loss & Audit Recovery Process**
1. **Simulate an Accidental Deletion**
   - Navigate to **C:\Internal Files**.
   - **Delete the folder** and empty the Recycle Bin.

2. **Perform Recovery from Remote Backup**
   - Open `wbadmin.msc`, select **Recover** > **Remote Shared Folder**.
   - Enter **Backup Location:** `\\DOMAINCONTROLL\Data Backup`.
   - Restore to **C:\Data Recovered**.

3. **Verify Recovery Integrity**
   - Open **File Explorer** > Check the **Data Recovered folder**.
   - Compare file integrity using PowerShell:
     ```powershell
     Get-FileHash "C:\Internal Files\file1.txt"
     Get-FileHash "C:\Data Recovered\file1.txt"
     ```
   - If hashes **match**, data is intact.
   - **If not, document data integrity failure** in an audit log.

---

### **✅ Step 4: Security Audit of Backup & Recovery Logs**
1. **Verify Backup & Recovery Logs in Event Viewer**
   - Open **Event Viewer** (`eventvwr.msc`).
   - Navigate to:
     ```
     Windows Logs > Application
     ```
   - **Filter by Event IDs:**
     - **Backup Successful** ➔ **Event ID 4**
     - **Backup Failed** ➔ **Event ID 49**
     - **Recovery Successful** ➔ **Event ID 123**
     - **Recovery Failed** ➔ **Event ID 124**
   - **Document findings in an audit report**.

2. **Check Backup Access Logs (Who Accessed Backup Files?)**
   - In Event Viewer, navigate to:
     ```
     Windows Logs > Security
     ```
   - **Filter for Event ID 4663 (File Access)**.
   - If **unauthorized users accessed backup files**, report a **security breach**.

---

## **📝 Audit Report Checklist**
✅ **Backup policies are defined and enforced** (`gpedit.msc`).  
✅ **Backup folder permissions are correctly configured** (`Get-Acl`).  
✅ **Backup process completed successfully** (`wbadmin.msc`).  
✅ **Backup logs verify successful execution** (`eventvwr.msc`, Event ID 4).  
✅ **Files restored successfully and integrity confirmed** (`Get-FileHash`).  
✅ **Access logs show no unauthorized users accessed backups** (Event ID 4663).  
✅ **Audit report generated documenting compliance gaps and findings**.

---

## **🏆 Compliance Frameworks Covered**
- **ISO 27001** (A.12.3: Backup policy compliance)  
- **PCI DSS** (Requirement 9.5: Secure data storage & recovery)  
- **NIST 800-53** (CP-9: Contingency planning for backups)  
- **HIPAA** (164.308(a)(7)(ii)(A): Data recovery procedures)  

---

## **🔥 Final Takeaways**
- This **audit-focused lab** enhances security by verifying backup and recovery **policy enforcement, logging, and security controls**.
- Instead of just performing a **backup & recovery**, this version **checks compliance, permissions, logs, and security risks**.
- **Great for an IT auditor portfolio**—aligns with **security best practices and real-world auditing tasks**.

---

Would you like me to include **PowerShell scripts** for automating these audit checks? 🚀
