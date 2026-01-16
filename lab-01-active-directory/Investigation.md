# Investigation – User Locked Out (Active Directory)

This document describes the troubleshooting process followed to identify
and resolve the authentication issue in the Active Directory lab.
The investigation was performed step by step, validating each layer
of the infrastructure.

The troubleshooting process was performed following a layered approach:
Network → DNS → Active Directory authentication.

---

## 1. Network Connectivity
- Inspected the network configuration of the Windows client.
- Verified IP addressing on both client and Domain Controller
- Confirmed both systems were on the same subnet


### Commands used:
- **ipconfig /all:** To check the Client and Windows Server IPs
- **ping <DC_IP_Address>:** To check connectivity between the Client and Windows Server.
- **ping <Client_IP_Address>:** To check connectivity between Windows Server and the Client.
- **nslookup lab.local <DC_IP_Address>:** To check if the problem is on the the Network or on the DNS.


### Findings:
- Network connectivity confirmed as functional
- The client had a valid IPv4 address.
- The IP address of one NIC belonged to a different subnet than the Domain Controller.
- The configured DNS server was incorrect and did not point to the Domain Controller.

This raised concerns regarding both routing and name resolution.

---

## 2. Network Adapter Configuration
- Identified multiple active network interfaces on the client
- Detected routing conflicts caused by NAT and Host-Only adapters
- Disabled non-essential adapters to ensure traffic used the lab network

### Commands used:
- **ipconfig /all:** To identify active network interfaces on the client.
- **Disable-NetAdapter -Name "Ethernet" -Confirm:$false:** To disable NAT Ethernet interface (NIC) 

### Result:
- Routing issues resolved

---

## 3. Firewall and Network Profile
- Identified Windows Defender Firewall blocking inbound traffic
- Confirmed client network profile was set to Public
- Changed profile to Private and created explicit ICMP allow rules
- Ensured bidirectional connectivity using ICMP after resolving firewall restrictions

### Commands used:
- **Set-NetFirewallProfile -Profile Domain,Private,Public -Enabled False:** To deactivate the Firewall
- **Set-NetConnectionProfile -InterfaceAlias "Ethernet" -NetworkCategory Private:** To change the client Interface from Public to Private
- **New-NetFirewallRule \`**
**-*DisplayName* "Allow ICMPv4 Inbound" \`**
**-*Name* "Allow ICMPv4-In" \`**
**-*Protocol* ICMPv4 \`**
**-*IcmpType* 8 \`**
**-*Direction* Inbound \`**
**-*Action* Allow \`**
**-*Profile* Any**: To set up an explicit ICMP rule for the correct testing of Ping function.

### Result:
- Firewall no longer blocked required traffic

---

## 4. DNS Resolution
- Client was using incorrect DNS servers (IPv6 automatic DNS)
- Active Directory SRV records could not be resolved
- Client DNS was manually configured to point to the Domain Controller

### Command used:
- **nltest /dsgetdc:lab.local:** To verify if the client failed to locate the domain controller.

### Result:
- Domain name and DC discovery restored

---

## 5. Active Directory Services
- Verified DNS and Netlogon services on the Domain Controller. DNS service was running
- Ensured SRV records were properly registered
- Active Directory Domain Services were operational.
- No critical errors were present in Event Viewer.

### Result:
- Domain Controller correctly advertised services
- Confirmed the issue originated from the client-side network and DNS configuration.

---

## 6. Kerberos Time Synchronization
- Identified significant time drift between client and Domain Controller
- Kerberos authentication failed due to clock skew
- Time service configuration and synchronization corrected

### Commands used:
- **w32tm /config /syncfromflags:domhier /update:** To synchronize the time with the one on the Domain Controller.
- **net stop w32time**
- **net start w32time**
- **w32tm /resync**

Result:
- Kerberos authentication stabilized

---

## 7. Validation
- User successfully logged in to the domain
- Password was changed interactively after successful authentication
- No further login issues observed

---

## Root Cause
The issue was caused by a combination of:
- Incorrect DNS configuration on the client
- Network adapter routing conflicts
- Firewall restrictions
- Kerberos authentication failures due to time desynchronization

---

## Final Status
✅ User access restored  
✅ Authentication services functioning correctly  
✅ Incident resolved and documented

This solution reflects standard Help Desk and Active Directory support practices.
