# Solution

The issue was resolved through a series of corrective actions addressing each contributing factor.

---

## 1. Network Cleanup
- Disabled unnecessary network adapters on the client
- Ensured both machines used the Host-Only lab network
- Verified bidirectional connectivity

---

## 2. Firewall Configuration
- Temporarily disabled firewall to confirm root cause
- Re-enabled firewall with explicit inbound ICMP rules
- Set correct network profile (Private)

---

## 3. DNS Configuration
- Configured client DNS to use the Domain Controller IP
- Disabled IPv6 DNS to prevent resolution conflicts
- Flushed DNS cache and verified name resolution

---

## 4. Domain Join
- Successfully joined the Windows 11 client to the `lab.local` domain
- Verified domain membership after reboot

---

## 5. User Account Recovery
- Reset the user password from the Domain Controller
- Removed the “Change password at next logon” flag to avoid login loop
- Verified account was not locked

---

## 6. Kerberos Time Fix
- Configured time synchronization hierarchy
- Synced client time from the Domain Controller
- Verified stable authentication

---

## 7. Validation
- User successfully logged in to the domain
- Password was changed interactively after successful authentication
- No further login issues observed

---

## Final Status
✅ User access restored  
✅ Authentication services functioning correctly  
✅ Incident resolved and documented

This solution reflects standard Help Desk and Active Directory support practices.
