# Lab: Active DirectoryDomain Services (AD DS) Deployment

**Date:** May 11, 2026

**Author:** Joseph Carlos

**Role:** Junior System Administrator (Simulation)



## Objective

To deploy and configure a primary Domain Controller (DC) to establish a centrailized identity and access management (IAM) system. This lab focuses on the installation, configuration, and promotion of a Windows Server 2022 environment.



## Tools Used

* **Windows Server 2022:** Primary Network Operating System.
* **Oracle VirtualBox:** Virtualization platform for environmment isolation.
* **Active Directory Domain Services (AD DS):** For centralized domain management.
* **DNS (Domain Name System):** Configured for local name resolution.



## Technical Breakdown



### Initial Server Configuration

* **System Identity:** Renamed the server to DC01 to comply with enterprise naming standards.
* **Static Networking:** Assigned a static IPV4 address (10.0.2.10) and configured the loopback address (127.0.0.1) for DNS to ensure service persistence.
* **Optimization:** Installed VirtualBox Guest Additions to improve VM performance and displaying scaling.



### Active Directory Installation & Promotion

* **Role Deployment:** Installed AD DS and DNS roles through Server Manager.
* **Forest Creation:** Established a new Active Directory Forest named carlos.local
* **Troubleshooting:** Identified and resolved a prerequisite failure by enforcing a complex password policy on the local Administrator account prior to promotion.



### Challenges Overcome

* **DNS Delegation Warning:** Diagnosed the "Authoritative Parent Zone" warning as a standard byproduct of an isolated lab environment and proceeded with the promotion.

* **Account Security Block:** Resolved a "local Administrator password required" error by updating the system account to meet domain complexity requirements.



### Enterprise identity & Automation

* **Organizational Hierarchy:** Created a custom Organizational Unit (OU) named **_Employees** to maintain a professional directory structure outside of default system containers.
* **Security Group Provisioning:** Established the **IT_Admins** Global Security Group to implement Role-Based Access Control (RBAC).
* **PowerShell AUtomation:** Developed and executed a PowerShell script utilizing a **for** loop to bulk-provision 1,000 yser accounts (User1 - User 1000) within the **_Employees** OU.
* **Scalability Simulation:** This phase simulates a large-scale corporate onboarding and demonstrates proficiency in System Administration and automation scripting.



### Automation Challanges Overcome

* **Parameter Binding Error:** Encountered a **ParameterBindingException** when attempting to use a non-standard color ("Gold") in the script.
* **Syntax Resolution:** Identified and corrected the parameter to "Yellow" using PowerShell color enumerators to ensure a clean execution.
*  **Network Status Discrepancy:** Observed the Windows "Globe" icon incorrectly reporting no internet access despite active connectivity.
*  **Connectivity Validation:** Validated the DNS service via browser testing and confirmed the icon as a common visual sync delay in isolated lab environments.
  

