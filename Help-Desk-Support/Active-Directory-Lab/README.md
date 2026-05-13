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

### Incidents & Resolutions

* **Incident:** Potential for poor VM performance and display lag during the initial Windows Server installation.
   * **Resolution:** Installed VirtualBox Guest Additions to provide driver optimization and hardware acceleration.



## Phase 2: AD DS Installation & Forest Promotion
In this phase, the standalone server was promoted to a primary Domain Controller to manage the **carlos.local** forest.

* **Role Deployment:** Installed the forest infrastructure and established the root domain.
* **Troubleshooting:** Enforced a **complex password policy** on the local Administrator account to bypass promotion blocks.
* **Tools Used:** 
    * **Server Manager:** For role-based deployment.
    * **AD DS & DNS:** Core directory and name resolution services.
    * **Active Directory Domain Services Configuration Wizard:** For forest promotion.

### Incidents & Resolutions

* **Incident:** Encountered a "Local Administrator password required" error that blocked the Forest Promotion process.
   * **Resolution:** Manually updated the system account to meet Domain Complexity Requirements, satisfying the security prerequisite.
* **Incident:** Received a DNS Delegation warning stating an "Authoritative Parent Zone" could not be found.
   * **Resolution:** Diagnosed this as a standard byproduct of an isolated lab environment; safely bypassed the warning to continue the promotion.



## Phase 3: Identity & Access Management (IAM)
This phase focused on building a professional directory structure to implement **Role-Based Access Control (RBAC)**.

* **Organizational Hierarchy:** Created the **_Employees** OU to separate corporate users from system containers.
* **Security Groups:** Established the **IT_Admins** Global Security Group to demonstrate proper permission delegation.
* **Tools Used:** 
    * **ADUC (Active Directory Users and Computers):** For GUI-based directory management.
    * **RBAC Principles:** To structure administrative access.

### Incidents & Resolutions

* **Incident:** Observed the Windows "Globe" icon (NCSI service) incorrectly reporting no internet access despite a functioning connection.
   * **Resolution:** Verified connectivity via browser testing (YouTube) and identified the icon as a visual sync delay common in new forest deployments.



## Phase 4: Automation & Scalability Simulation
To simulate a real-world corporate onboarding event, I utilized scripting to automate the creation of a large-scale user database.

* **Bulk Provisioning:** Executed a script using a **for loop** to generate **1,000 user accounts** (User1 - User1000).
* **Debugging:** Resolved a **ParameterBindingException** by correcting color enumerators and validated connectivity via browser testing.
* **Tools Used:** 
    * **PowerShell:** For automation and logic.
    * **PowerShell ISE:** For script development and debugging.
    * **Microsoft Edge:** To validate DNS/Internet connectivity.
 
### Incidents & Resolutions

* **Incident:** Attempted to run the multi-line automation script in the interactive console, which disabled execution shortcuts like F5.
   * **Resolution:** Transitioned the code to the **PowerShell ISE Script Pane**, enabling full debugging and play functionality.
* **Incident:** The script failed with a **ParameterBindingException** because the color "Gold" is not a standard PowerShell enumerator.
   * **Resolution:** Researched the **System.ConsoleColor** list and corrected the code to use "Yellow", allowing the script to complete the 1,000-user creation.


