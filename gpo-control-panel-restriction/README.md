# Group Policy Lab — Marvel OU Control Panel Restriction

## Objective
Use Active Directory Group Policy to prevent users in the Marvel organizational unit (OU) from accessing Control Panel and Windows Settings on a domain-joined Windows 11 workstation.

## Lab environment
- Windows Server domain controller: DC01
- Active Directory Domain Services and Group Policy Management
- Marvel and DC organizational units
- Domain-joined Windows 11 virtual machine
- Test domain account: Tony Stark (`tstark`)

## Implementation
1. Created a GPO named `Marvel - Block Control Panel`.
2. Linked the GPO to the Marvel OU.
3. Edited **User Configuration > Policies > Administrative Templates > Control Panel**.
4. Enabled **Prohibit access to Control Panel and PC settings**.
5. Signed into the Windows 11 domain workstation with the Marvel test account.
6. Attempted to open Control Panel with `control`.

## Result
**Passed:** Windows displayed a restriction message instead of opening Control Panel. This confirmed the restriction was effective for the tested Marvel user.

## Troubleshooting and verification
- `gpupdate /force` requests a policy refresh.
- `gpresult /r` can be used to inspect applied user GPOs.
- Signing out and back in can help user policies take effect.

## Key takeaways
- OU links define the scope in which a GPO may apply.
- User Configuration settings follow the domain user, subject to security filtering and policy processing.
- A configured policy should always be tested on a domain-joined endpoint.

> This is a hands-on educational lab using fictional test accounts, not a production deployment.
