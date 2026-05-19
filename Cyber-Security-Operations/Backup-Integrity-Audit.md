# Backup Verification & Data Integrity

This log documents internal data resiliency audits and disaster recovery verifications conducted on core identity infrastructure assets.

---

## Incident #1049: Domain Controller Disaster Recovery Gap Identification
**Date:** May 18, 2026  
**Category:** Security Operations & Data Resiliency  
**Priority:** High (Critical Infrastructure Gap)

### **The Detection**
Conducted a systemic infrastructure audit via administrative PowerShell on Domain Controller 'DC01' utilizing the 'Get-WindowsFeature' command to verify the operational readiness of native backup systems.

### **The Finding**
The interrogation of the operating system package state revealed a critical vulnerability:
* **Identified Security Gap:** The 'Windows-Server-Backup' feature returned an install state of **Available** (Uninstalled).
* **Risk Analysis:** Operating a primary Domain Controller without a local or networked disaster recovery backup model introduces catastrophic risk. A hardware failure, database corruption, or ransomware deployment would result in permanent loss of the Active Directory database ('NTDS.dit'), breaking authentication across the entire organization.

### **The Remediation & Verification Steps**
1. **Feature Deployment:** Executed 'Install-WindowsFeature Windows-Server-Backup' via elevated PowerShell to force-install the native bare-metal recovery sub-system.
2. **Task Modification:** Altered task properties within Task Scheduler to enable **"Allow task to be run on demand"**, bypassing default operating system restrictions.
3. **Operational Verification:** Manually executed the 'Microsoft-Windows-WindowsBackup' task on-demand. Verified the status transitioned to **Running** and confirmed via the Server Backup console that system-state files were actively being committed to the local storage directory ('C:\BackupShare').
4. **Policy Recommendation:** Proposed a formal Backup Policy requiring automated nightly system-state backups stored in an immutable, offsite repository.

### **Security+ Knowledge Mapping**
* **Objective 2.0:** Resiliency and Recovery (Backup strategies, backup types, and data integrity verification).
* **Objective 4.0:** Security Operations (Disaster recovery posture and infrastructure hardening).
