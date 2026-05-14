**Date:** May 11, 2026  
**Author:** Joseph Carlos  
**Role:** Junior System Administrator (Simulation)



### Project Overview
This lab demonstrates the end-to-end deployment of a **Windows Server 2022** environment. The project is structured into five distinct phases, covering initial provisioning, domain promotion, security structuring, and large-scale automation.



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



## Phase 5: Client-Side integration & Policy Enforcement
   The goal of this phase was to join a Windows 11 workstation to the **carlos.local** domain and verify that administrative security controls are successfully enforced on remote assets.

* **Client Provisioning:** Deployed a Windows 11 Pro VM and optimized it for the lab environment using VirtualBox Guest Additions for seamless scaling and driver performance.
* **Domain Integration:** Performed a "Network Handshake" by configuring a static DNS pointing to the Domain Controller (10.0.2.10) and successfully joined the workstation to the **carlos.local** forest.
* **Security Validation:** Authenticated as a domain user (User67) and verified Least Privilege by confirming the user was restricted from accessing the Control Panel and administrative terminals.
* **Tools Used:**
   * **Group Policy Management (GPMC):** To create and link security objects to the **_Employees** OU.
   * **Active Directory Users & Computers (ADUC):** For administrative password resets and user account management.
   * **Command Line (gpresult/r):** To verify policy application on the client machine.
 
### Incidents & Resolutions

* **Incident:** Encountered a "Media disconnected" status and "General Failure" when attempting to pink the Domain Controller.
   * **Resolution:** Identified that the virtual network adapter was disconnected during the OOBE bypass; re-enabled the Cable Connected status in VirtualBox and tansitioned from NAT to Internal Network **(Intnet)**
* **Incident:** Group Policy Objects (GPOs) were showing as **N/A** on the client machine despite a successful domain join.
   * **Resolution:** Diagnosed the issue as a "Link Gap"; the policy existed but was n ot physically linked to the **_Employees** OU. Manually established the link in GPMC and ran **gpupdate /force** to sync the workstation.
* **Incident:** The GPO Settings report failed to load on the server due to **IE Enhanced Security Configuration** blocking the internal report display.
   * **Resolution:** Temporarily disabled IE Hardening for Administrators within Server Manager, allowing the GPMC to generate the report and verify the "Control Panel" restriction was active.

