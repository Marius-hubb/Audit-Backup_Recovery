# Auditing Data Backup & Recovery in Windows

## Description
This lab demonstrates how to **audit** data backup and recovery processes in Windows. The focus is on ensuring compliance with **ISO 27001, PCI DSS, NIST 800-53, and HIPAA** by verifying backup integrity, access controls, and logging mechanisms.

## Lab Objectives
- **Verify** backup configurations and storage locations.
- **Assess** access controls and security policies for backup security.
- **Ensure** backup integrity using audit techniques.
- **Analyze** event logs for backup and restore activities.

---

## Lab Tasks

### Step 1: Verify Backup Completion & Storage Location
1. **Check Backup Configuration**
   - Open **Windows Server Backup (`wbadmin.msc`)**.
   - Navigate to **Local Backup** > **View Backups**.
   - Identify the latest backup and document the following:
     - **Date and time of the last backup**
     - **Storage location** (`\DOMAINCONTROLL\Data Backup` or another directory)
     - **Backup status (Successful/Failed)**
   - **Audit Task**: Record findings in the audit report.

2. **Confirm Backup File Integrity**
   - Navigate to the backup storage folder (`C:\BackupLocation` or `\DOMAINCONTROLL\Data Backup`).
   - Verify the presence of the backup files.
   - Use **PowerShell** to check file integrity:
     ```powershell
     Get-FileHash "C:\BackupLocation\BackupFile.bak"
     ```
   - Compare the hash value with the original to confirm no corruption.
   - **Audit Task**: Document integrity verification results.

---

### Step 2: Security Audit of Backup Access Permissions
1. **Review Folder Permissions**
   - Navigate to **File Explorer**, right-click **Backup Folder** (`C:\BackupLocation`), and select **Properties**.
   - Click the **Security** tab and check the assigned permissions.
   - **Ensure the following roles have appropriate permissions:**
     - **Administrators** → Full Control
     - **Backup Operators** → Modify & Read
     - **Authenticated Users** → Read Only
     - **Everyone** → **Should NOT have access**
   - **Audit Task**: Document any misconfigurations or excessive permissions.

2. **Enable & Review Backup Access Logs**
   - Open **Local Security Policy (`secpol.msc`)**.
   - Navigate to:
     ```
     Security Settings > Advanced Audit Policy Configuration > Object Access > Audit File System
     ```
   - Enable **Success & Failure Logging** for the backup folder.
   - Open **Event Viewer (`eventvwr.msc`)**, navigate to:
     ```
     Windows Logs > Security
     ```
   - **Filter for Event ID 4663 (File Access)**.
   - **Audit Task**: Identify unauthorized access attempts and document findings.

---

### Step 3: Review Backup & Recovery Logs
1. **Verify Backup Logs in Event Viewer**
   - Open **Event Viewer (`eventvwr.msc`)**.
   - Navigate to:
     ```
     Applications and Services Logs > Microsoft > Windows > Backup
     ```
   - **Filter for Event IDs:**
     - **Backup Successful** → Event ID 4
     - **Backup Failed** → Event ID 49
   - **Audit Task**: Document log details in the audit report.

2. **Check Recovery Logs**
   - Navigate to **Event Viewer** and filter for:
     - **Recovery Successful** → Event ID 123
     - **Recovery Failed** → Event ID 124
   - **Audit Task**: Verify recovery attempts and confirm success/failure.

---
