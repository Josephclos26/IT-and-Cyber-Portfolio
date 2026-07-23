# Active Directory User Automation, SMB Share Provisioning & RBAC Validation

**Date:** July 2026  
**Author:** Joseph Carlos  
**Role:** Junior System Administrator (Simulation)  

---

## Project Overview
This project demonstrates advanced Active Directory (AD) administration following initial domain deployment. It covers automated user attribute management via PowerShell, secure departmental network share provisioning using SMB and NTFS permissions, and security validation through Role-Based Access Control (RBAC) testing.

---

## Phase 1: Bulk User Attribute Automation

### Objective
Populate essential corporate metadata (Title, Department, Company, Description) and asset tracking tags for domain users to simulate automated onboarding and asset tracking.

### Implementation
Executed a PowerShell loop targeting domain users to assign standardized attributes and custom employee IDs:

```powershell
# Define target users and global attributes
$Users = "User1", "User2", "User3", "User4", "User5"

foreach ($User in $Users) {
    Set-ADUser -Identity $User `
        -Title "Marketing Specialist" `
        -Department "Marketing" `
        -Company "Carlos Corp" `
        -Description "Standard Domain User - Marketing Dept" `
        -EmployeeID "ASSET-2026-$User"
}
