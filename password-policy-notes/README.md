# Active Directory Password Policy — Troubleshooting Notes

## Objective
Understand domain password policies, OU-linked GPOs, and per-account password-change requirements.

## Topics explored
- Minimum password length, complexity, password history, and account lockout settings
- Difference between a standard domain password policy and a GPO linked only to an OU
- Difference between password requirements and **User must change password at next logon**
- Signing out and back in to test account changes

## Important distinctions
- Standard domain-account password policy is sourced from applicable domain-root-linked policy, not an arbitrary OU-linked password GPO.
- Different password policies for different users or groups can be implemented using fine-grained password policies (FGPP).
- Password complexity requirements do **not** automatically force a password change at the next sign-in.
- The **User must change password at next logon** flag is a separate per-account setting.

## Verification still needed
Run `Get-ADDefaultDomainPasswordPolicy` on DC01 and verify the effective domain settings. This exercise is documented as **learning and troubleshooting**, not a fully validated password-policy deployment.
