# Auditing Data Backup & Recovery in Windows

## Description
This lab demonstrates how to **audit** data backup and recovery processes in Windows. The focus is on ensuring compliance with **ISO 27001, PCI DSS, NIST 800-53, and HIPAA** by verifying backup integrity, access controls, and logging mechanisms.

## Lab Objectives
- Verify backup configurations and storage locations.
- Assess access controls and security policies for backup security.
- Analyze event logs for backup and restore activities.

---

## Lab Walk Through

#### Verify Backup Completion & Storage Location
   - Windows Server Backup > Local Backup
   - Backup location is set to the folder \\\DOMAINCONTROLL\Data Backup
<p align="center">
<br/>
<img src="https://i.imgur.com/Kfaz66R.png" height="50%" width="80%" alt="Disk Sanitization Steps"/>
<br />

#### Security Audit of Backup Access Permissions
   - Reviewing Backup Folder Permissions
<p align="center">
<br/>
<img src="https://i.imgur.com/xhT0mpO.png" height="50%" width="80%" alt="Disk Sanitization Steps"/>
<br/>

#### Enable & Review Backup Access Logs
   - Open **Local Security Policy**
   - Navigate to:
     ```
     Security Settings > Advanced Audit Policy Configuration > Object Access > Audit File System
     ```
   - Enable **Audit File System**.
  <p align="center">
<br/>
<img src="https://i.imgur.com/IcpHtWd.png" height="50%" width="80%" alt="Disk Sanitization Steps"/>
<br/>
   

#### Review Backup  & Recovery Logs
   - Open **Event Viewer (`eventvwr.msc`)**.
   - Navigate to:
     ```
     Applications and Services Logs > Microsoft > Windows > Backup
     ```
   - **Filter for Event IDs:**
     - **Backup Successful** → Event ID 4
     - **Backup Failed** → Event ID 49

  <p align="center">
<br/>
<img src="https://i.imgur.com/5l6Eele.png" height="50%" width="80%" alt="Disk Sanitization Steps"/>
<br/>

   - Navigate to:
      ```
     Windows Logs > Security
     ```
   - Filter for Event ID 4663 (File Access).
  <p align="center">
<br/>
<img src="https://i.imgur.com/DRUd8gk.png" height="50%" width="80%" alt="Disk Sanitization Steps"/>
<br/>
     
#### Perform Recovery Test in Windows Server Backup
  <p align="center">
<br/>
<img src="https://i.imgur.com/iTC8jJQ.png" height="50%" width="80%" alt="Disk Sanitization Steps"/>
<br/>

#### Check Recovery Logs
   - Navigate to **Event Viewer** and filter for:
     - **Recovery Successful** → Event ID 123
     - **Recovery Failed** → Event ID 124
   - **Audit Task**: Verify recovery attempts and confirm success/failure.



## Audit Report Checklist
- **Backup process completed successfully (`wbadmin.msc`).**  
- **Backup logs verify successful execution (`eventvwr.msc`, Event ID 4).**  
- **Access permissions properly configured (No 'Everyone' access).**  
- **Access logs reviewed for unauthorized attempts (Event ID 4663).**  
- **Audit report generated documenting compliance gaps and findings.**  


2. **Check Recovery Logs**
   - Navigate to **Event Viewer** and filter for:
     - **Recovery Successful** → Event ID 123
     - **Recovery Failed** → Event ID 124
   - **Audit Task**: Verify recovery attempts and confirm success/failure.

---
