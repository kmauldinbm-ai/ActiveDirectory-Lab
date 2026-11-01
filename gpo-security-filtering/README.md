# Group Policy Lab — Targeted Control Panel Restriction with Security Filtering

## Objective
Apply a Control Panel restriction to one selected user in the DC OU without requiring a separate OU.

## Environment
- DC01: Active Directory and Group Policy Management
- Domain-joined Windows 11 workstation
- DC OU
- Test accounts: Bruce Wayne and Clark Kent

## Implementation
1. Created a **Global Security** group named `SG_DC_RestrictedUsers` in Active Directory Users and Computers.
2. Added Bruce Wayne as a member.
3. Created the GPO `DC - Restricted Control Panel` and linked it to the DC OU.
4. Enabled **User Configuration > Policies > Administrative Templates > Control Panel > Prohibit access to Control Panel and PC settings**.
5. Used **Scope > Security Filtering** to target `SG_DC_RestrictedUsers`, with appropriate Read and Apply Group Policy permissions.
6. Signed into the Windows 11 VM as Bruce Wayne and attempted to open Control Panel.

## Result
**Passed for Bruce Wayne:** Control Panel was blocked after signing in as Bruce.

**Not yet verified:** The planned negative test with Clark Kent (not a member of the restricted group) was not completed. Therefore, the lab demonstrates successful restriction for the targeted user, but does not yet conclusively prove exclusion of nonmembers.

## Troubleshooting knowledge
- Verify the GPO link and that it is enabled.
- Inspect **Scope > Security Filtering** and **Delegation > Advanced** for Read and Apply Group Policy permissions.
- Confirm the user's group membership in ADUC.
- Sign out and back in after group membership changes to refresh the logon token.
- Use `gpresult /r` to investigate which user policies actually applied.

## Concepts learned
- Global vs. Domain Local security group scopes
- GPO linking vs. security filtering
- Group membership and Windows logon tokens
- Least-privilege targeting of user policies

## Next validation
Sign into the Windows 11 workstation as Clark Kent, run `control`, and confirm that Control Panel remains accessible. Inspect `gpresult /r` for the filtered GPO if the outcome is unexpected.
