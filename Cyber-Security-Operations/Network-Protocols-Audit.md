# Network Protocols & Port Audit
This log documents proactive network surface area audits conducted within the **carlos.local** domain environment to verify the decommissioning of legacy, unencrypted plaintext protocols.

---

## Incident #1047: Layer 4 Port & Protocol Baseline Audit
**Date:** May 18, 2026  
**Category:** Security Architecture & Network Security  
**Priority:** Low (Proactive Hardening Verification)

### **The Detection**
Utilized native command-line utilities ('netstat') with administrative privileges on Domain Controller 'DC01' to map all active TCP/UDP daemons currently in a `LISTENING' state.

### **The Finding**
An analysis of the open socket connections confirmed that the domain controller is securely running core infrastructure services while keeping legacy cleartext pathways closed:
* **Active Infrastructure Ports:** TCP 53 (DNS), TCP 88 (Kerberos Authentication), TCP 389 (LDAP Directory Services), and TCP 445 (SMB File Sharing).
* **Hardening Verification:** Plaintext protocol listeners such as TCP 23 (Telnet), TCP 21 (FTP), and TCP 80 (HTTP) were verified as **inactive/disabled**, reducing the risk of packet-sniffing attacks.

### **The Remediation & Verification Steps**
1. **Socket Interrogation:** Executed 'netstat -an | findstr "LISTENING"' to dump the active protocol control blocks.
2. **Attack Surface Reduction:** Verified that no unencrypted management consoles are exposed on the local network interface.

### **Security+ Knowledge Mapping**
* **Objective 2.0:** Secure Protocols (Differentiating between cleartext and encrypted protocols like HTTPS, SSH, and secure AD services).
* **Objective 3.0:** Network Security Architecture (Attack surface minimization and port management).
