# Problem Description – User Locked Out

## Reported Issue
A domain user reported being unable to log in to their workstation. The system indicated that the user account required a password change, but the login process repeatedly failed, preventing access to the desktop.

---

## User Impact
- User unable to access the workstation
- Business tasks blocked due to lack of domain authentication
- Repeated login attempts did not resolve the issue

---

## Initial Symptoms
- Login attempts prompted: “The user's password must be changed before signing in”
- After entering a new password, the system returned to the same prompt
- Domain join attempts initially failed with:
  - “An Active Directory Domain Controller for the domain could not be contacted”

---

## Scope
- Affected user: `jperez`
- Affected system: Windows 11 Pro domain-joined workstation
- Authentication source: Active Directory domain `lab.local`

The issue required investigation across networking, DNS, Active Directory, and authentication services.
