# Technical Support & Operations Log
This log documents real-time troubleshooting, system maintenance, and "Break/Fix" scenarios performed within the **carlos.local** lab environment. Each entry follows a IT ticketing format.


## Ticket #1042: Restricted Access Failure (GPO)
**Date:** May 14, 2026
**Status:** Resolved
**Priority:** Medium (Security Compliance)



### **The Issue**
A user in the Warehouse department (User67) reported they could suddenly access the full Windows Control Panel. This should be blocked by company policy to prevent unauthorized system changes.

### **The Investigation**
* **Client Verification:** Logged into the workstation and ran 'gpresult /r'.\
* **Discovery:** Confirmed the 'Lab_Security_Policy' was showing as N/A under "Applied Group Policy Objects."
* **Connectivity Check:** Verified the workstation could still communicate with the Domain controller (DC01) via 'ping'.

### **The Root Cause**
The **Group Policy Link** for the '_Employees' Organizational Unit (OU) was found to be disabled on the Domain Controller. This stopped the security rules from being sent to the workstations in that department.

### **The Resolution**
1. **GPMC:** Re-enabled the link for 'Lab_Security_Policy' on the DC.
2. **Sync:** Forced a policy refresh on the client using 'gpupdate /force'.
3. **Verification:** Re-ran 'gpresult /r' and confirmed the policy is now **Applied**. Control Panel access is successfully restricted.
