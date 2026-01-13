# Diagnosis

A structured troubleshooting approach was followed, validating each layer involved in domain authentication.

---

## 1. Network Connectivity
- Verified IP addressing on both client and Domain Controller
- Confirmed both systems were on the same subnet
- Ensured bidirectional connectivity using ICMP after resolving firewall restrictions

Result:
- Network connectivity confirmed as functional

---

## 2. Network Adapter Configuration
- Identified multiple active network interfaces on the client
- Detected routing conflicts caused by NAT and Host-Only adapters
- Disabled non-essential adapters to ensure traffic used the lab network

Result:
- Routing issues resolved

---

## 3. Firewall and Network Profile
- Identified Windows Defender Firewall blocking inbound traffic
- Confirmed client network profile was set to Public
- Changed profile to Private and created explicit ICMP allow rules

Result:
- Firewall no longer blocked required traffic

---

## 4. DNS Resolution
- Client was using incorrect DNS servers (IPv6 automatic DNS)
- Active Directory SRV records could not be resolved
- Client DNS was manually configured to point to the Domain Controller

Result:
- Domain name and DC discovery restored

---

## 5. Active Directory Services
- Verified DNS and Netlogon services on the Domain Controller
- Ensured SRV records were properly registered

Result:
- Domain Controller correctly advertised services

---

## 6. Kerberos Time Synchronization
- Identified significant time drift between client and Domain Controller
- Kerberos authentication failed due to clock skew
- Time service configuration and synchronization corrected

Result:
- Kerberos authentication stabilized

---

## Root Cause
The issue was caused by a combination of:
- Incorrect DNS configuration on the client
- Network adapter routing conflicts
- Firewall restrictions
- Kerberos authentication failures due to time desynchronization

No single misconfiguration caused the problem; it was the result of multiple layered issues.
