# Technical Support & Operations Log
This log documents real-time troubleshooting, system maintenance, and "Break/Fix" scenarios performed within the **carlos.local** lab environment. Each entry follows a IT ticketing format.

---

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

---

## Ticket #1043: Account Lockout - User67
**Date:** May 14, 2026
**Status:** Resolved
**High (User Productivity)**



### **The Issue**
User reported they are unable to log in and are receving an error message stating the account is "currently locked out."

### **The Root Cause** 
User exceeded the maximum number of failed login attempts, triggering the Domain Password Policy lockout mechanism.

### **The Resolution**
1. Accessed Active Directory Users and Computers on DC01.
2. Located User67 and verified the account was locked under the Account tab.
3. Manually unlocked the account and verified the user regained access to the workstation.

---

## Ticket #1044: Password Reset Request
**Date:** May 14, 2026
**Status:** Resolved
**Low (Standard Request)**



### **The Issue**
User reported they had forgotten their domain password and were unable to access their workstation.

### **The Resolution**
1. Verified user identity and performed a password reset for **User67** in Active Directory.
2. Enabled **"User must change password at next logon"** to ensure account privacy.
3. **TIP:** Advised a full system restart to clear cached credentials and ensure the client synchronized with the Domain Controller's new password data.
4. Confirmed user successfully updated their password and regained system access.



## Ticket #1045: VirtualBox Bridge & ICMP Connectivity Verification
**Date:** July 21, 2026
**Status:** Resolved
**Priority:** Medium (Infrastructure / Network Setup)

### **The Issue**
New lab VMs (Windows Server and Windows 11 Client) were unable to communicate over the network. Pings from the Windows 11 client (`192.168.0.20`) to the Windows Server (`192.168.0.10`) were timing out despite both machines being configured on the same subnet (`192.168.0.0/24`).

### **The Investigation**
* **Hardware & Link Check:** Verified physical network adapter binding to the external TP-Link switch and enabled `Promiscuous Mode: Allow VMs` in VirtualBox bridged settings.
* **IP Configuration:** Assigned static IPs (`192.168.0.10` for Server, `192.168.0.20` for Client) and verified interface status using `ipconfig`.
* **Firewall Isolation:** Tested ICMP traffic using `ping 192.168.0.10` from the client; confirmed packet drop at the server host firewall.

### **The Root Cause**
The Windows Server host firewall was enforcing default inbound security rules, dropping ICMP Echo Request (ping) packets from non-local subnets / unauthorized services.

### **The Resolution**
1. **Firewall Rule Management:** Executed PowerShell as Administrator on the Windows Server to enable ICMP traffic through the built-in firewall display group:
   ```powershell
   Enable-NetFirewallRule -DisplayGroup "File and Printer Sharing"
