# Enterprise DHCP Configuration & Network Hardening
This log documents the deployment of centralized dynamic IP addressing infrastructure and corresponding Blue Team defensive baseline.

---

## Incident #1050: Centralized IP Infrastructure Deployment
**Date:** May 18, 2026  
**Category:** Systems Administration & Network Architecture  
**Priority:** Medium

### **The Mission**
Migrate the enterprise lab network away from unmanaged, decentralized static IP addressing to a centralized, scalable **DHCP Server** model directly by the Active Directory Domain Controller ('DC01').

### **The Architecture Implementation**
1. **Role Installation:** Deployed the 'DHCP Server' role via Windows Server Manager binaries.
2. **Active Directory Authorization:** Executed post-install integration to register the DHCP server within the AD schema. 
   * *Blue Team Value:* This prevents unauthorized "rogue" DHCP servers from joining the domain and executing rogue lease hijacking or Man-in-the-Middle (MitM) sniffing vectors.
3. **Subnet Scope Design:** Built an address pool designated as 'Corporate-Workstation-Pool' using a '192.168.10.0/24' schema.
4. **Infrastructure Protection:** Configured an explicit exclusion range from '192.168.10.1' to '192.168.10.50' to safeguard core infrastructure assets (gateways, domain controllers, managed switches) from IP address duplication conflicts.
5. **Lease Matrix Hardening:** Optimized standard lease times down to **1 Day** to increase address recycling efficiency and mitigate **DHCP Starvation** resource exhaustion attacks.

---

### **Operational Notes for Lab Topology**
* **Subnet Alignment:** Note that the host server interface currently operates on a '10.0.2.X' broadcast domain. Full end-to-end lease delivery to the '192.168.10.X' workstation pool requires either a multi-homed NIC configuration on 'DC01' or an explicit DHCP Relay Agent (IP Helper) rule configured on the core virtual router interface.
