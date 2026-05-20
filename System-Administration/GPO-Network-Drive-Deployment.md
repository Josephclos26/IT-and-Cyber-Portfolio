# GPO-Network-Drive-Deployment

## Project Overview
This project demonstrates the configuration and deployment of automated network storage mapping using Windows Server 2022 Group Policy Objects (GPOs). To centralize files, prevent local data loss from hardware failure, and secure sensitive departmental data, a dual-layer storage architecture was implemented across the domain.

---

## Storage Architecture Design

The storage infrastructure is split into two operational tiers:

| Drive Letter | Share Name | Target Audience | Scope / Security Mechanism | Business Purpose |
| :---: | :--- | :--- | :--- | :--- |
| **W:** | Warehouse Share | All Domain Users | Global Inheritance (Domain-Linked GPO) | Centralized collaboration, shift handovers, and corporate SOP distribution. |
| **P:** | Packing Department | 'SG-Packing-Dept' Members | **Item-Level Targeting** (Conditional Logic) | Isolated storage for outbound manifests and packing logs. Restricted from non-departmental eyes. |

---

## Configuration & Implementation Steps

### 1. Physical Directory & SMB Share Provisions
* Provisioned local directories on the Domain Controller ('C:\CompanyShare' and 'C:\PackingShare').
* Configured network sharing properties, opening universal naming convention (UNC) broadcast paths:
  * '\\DC01\CompanyShare'
  * '\\DC01\PackingShare'
* Applied Full Control share permissions to the network layer.

### 2. RBAC Group Provisioning
* Created a global security group named **'SG-Packing-Dept'**.
* Assigned test user objects (e.g., 'User67') to the security group to establish role-based identities before policy deployment.

### 3. GPO Orchestration & Item-Level Targeting
* Enacted a centralized policy container named **'GPO-Map-Network-Drive'** linked directly to the root of the domain.
* Navigated through the **User Configuration** preference hives to isolate mapping execution directly to authenticating users rather than static hardware endpoints.
* Applied conditional logic using the Group Policy **Item-Level Targeting** engine to bind the 'P:\' drive exclusively to security principal **'SG-Packing-Dept'**.

---

## Client-Side Verification Testing (Runbook)

To verify the deployment from an endpoint terminal, execute the following validation steps on a Windows 11 workstation:

1. Log in to the workstation as a domain user mapped to the packing role (e.g., 'User67').
2. Open the Command Prompt ('cmd') and manually force an immediate update of the client policy environment against the Domain Controller:
   ```cmd
   gpupdate /force
