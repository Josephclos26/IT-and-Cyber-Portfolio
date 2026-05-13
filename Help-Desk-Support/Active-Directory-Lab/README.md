**Date:** May 11, 2026  
**Author:** Joseph Carlos  
**Role:** Junior System Administrator (Simulation)



### Project Overview
This lab demonstrates the end-to-end deployment of a **Windows Server 2022** environment. The project is structured into four distinct phases, covering initial provisioning, domain promotion, security structuring, and large-scale automation.



## Phase 1: Environment Provisioning & Networking
The goal of this phase was to establish a stable, isolated virtual foundation for the **Domain Controller**.

* **System Identity:** Renamed the host to **DC01** to comply with enterprise naming standards.
* **Networking:** Configured a **Static IPv4 address (10.0.2.10)** and a **Loopback address (127.0.0.1)** to ensure DNS persistence.
* **Tools Used:** 
    * **Oracle VirtualBox:** For environment isolation.
    * **Windows Server 2022:** Base Operating System.
    * **VirtualBox Guest Additions:** For driver optimization and scaling.



## Phase 2: AD DS Installation & Forest Promotion
In this phase, the standalone server was promoted to a primary Domain Controller to manage the **carlos.local** forest.

* **Role Deployment:** Installed the forest infrastructure and established the root domain.
* **Troubleshooting:** Enforced a **complex password policy** on the local Administrator account to bypass promotion blocks.
* **Tools Used:** 
    * **Server Manager:** For role-based deployment.
    * **AD DS & DNS:** Core directory and name resolution services.
    * **Active Directory Domain Services Configuration Wizard:** For forest promotion.



## Phase 3: Identity & Access Management (IAM)
This phase focused on building a professional directory structure to implement **Role-Based Access Control (RBAC)**.

* **Organizational Hierarchy:** Created the **_Employees** OU to separate corporate users from system containers.
* **Security Groups:** Established the **IT_Admins** Global Security Group to demonstrate proper permission delegation.
* **Tools Used:** 
    * **ADUC (Active Directory Users and Computers):** For GUI-based directory management.
    * **RBAC Principles:** To structure administrative access.



## Phase 4: Automation & Scalability Simulation
To simulate a real-world corporate onboarding event, I utilized scripting to automate the creation of a large-scale user database.

* **Bulk Provisioning:** Executed a script using a **for loop** to generate **1,000 user accounts** (User1 - User1000).
* **Debugging:** Resolved a **ParameterBindingException** by correcting color enumerators and validated connectivity via browser testing.
* **Tools Used:** 
    * **PowerShell:** For automation and logic.
    * **PowerShell ISE:** For script development and debugging.
    * **Microsoft Edge:** To validate DNS/Internet connectivity.
