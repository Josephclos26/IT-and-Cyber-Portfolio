# Cyber Security & Audit Log

This log documents proactive security audits, identity access management (IAM) compliance, and incident response operations within the **carlos.local** environment.

---

## Incident #1045: Privilege Escalation Remediation
**Date:** May 15, 2026  
**Category:** Identity & Access Management (IAM)  
**Priority:** Critical

### **The Detection**
Conducted a manual access review of highly privileged security groups within Active Directory to ensure alignment with the **Principle of Least Privilege (PoLP)**.

### **The Finding**
Discovered that a standard warehouse user account (**User67**) was incorrectly nested within the **Domain Admins** group. This configuration bypasses standard access controls and represents a severe privilege escalation risk.

### Potential Causes
* **Privilege Creep:** A standard user is granted temporary admin access for a specific task or software update, but the account is mistankenly never removed after completion.
* **Legacy Software Requirements:** Poorly enginered applications sometimes demand administrative rights to run. Accounts are improperly added to the admin group to bypass granular permission troubleshooting.
* **Malicious Escalation:** An attacker or rogue insider compromises a standard account and intentionally forces a vertical privilege escalation to establish a permanent foothold.

### **Containment & Resolution**
1. **Access Revocation:** Immediately removed **User67** from the Domain Admins group to restrict unauthorized administrative access.
2. **Verification:** Confirmed that only the built-in Administrator account retains membership in the group.
3. **Policy Recommendation:** Proposed implementing quarterly User Access Reviews (UAR) to prevent future permission creep.

### **Security+ Knowledge Mapping**
* **Objective 1.2:** Analyzing organizational security posture (Threats & Vulnerabilities).
* **Objective 3.0:** Implementing Identity and Access Management concepts.
