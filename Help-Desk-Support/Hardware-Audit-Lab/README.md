# Lab: Hardware & System Health Audit
**Date:** May 11, 2026
**Author:** Joseph Carlos
**Role:** Tier 1 IT Support Technician (Simulation)

## Objective
To perform a comprehensive hardware inventory and health assessment of a primary workstation to ensure operational readiness and data integrity.

## Tools Used
* **Windows PowerShell:** For system health queries.
* **System Information (msinfo32):** For hardware specifications.
* **Command Prompt:** For network configuration details.

## Steps Taken

### 1. Hardware Inventory
I accessed the system specifications to verify the resources available for virtualization and security tasks.
* **CPU:** AMD Ryzen 5 5600X 6-Core Processor
* **RAM:** 16GB DDR4
* **GPU:** AMD Radeon RX 6650 XT

### 2. Storage Health Check (S.M.A.R.T. Status)
I used PowerShell to verify the physical health of the primary drive to prevent data loss.
* **Command:** `Get-StorageReliabilityCounter` or `wmic diskdrive get status`
* **Result:** OK

### 3. Network Configuration Audit
I verified the local network settings to ensure proper connectivity for future lab environments.
* **Local IP Address:** 192.168.1.0/24
* **Subnet Mask:** 255.255.255.0

## Results & Conclusion
The system is fully operational with healthy storage and correct network configurations. This workstation is cleared for the deployment of a Virtual Lab environment.              
