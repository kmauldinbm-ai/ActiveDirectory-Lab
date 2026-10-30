# Active Directory Group Policy Drive-Mapping Lab

A hands-on lab using Group Policy Preferences to map department shares for the right users based on Active Directory security-group membership.

## Lab environment

- **Domain:** `multiverse.test`
- **Domain controller and file server:** `DC01` running Windows Server 2025
- **Client:** Windows 11 Enterprise joined to the domain
- **Virtualization:** Oracle VirtualBox
- **Shares:** `\\DC01\AvengersShare` and `\\DC01\XMenShare`
- **Scope OU:** `Marvel`
- **Security groups:** `Avengers` and `X-Men`

## What I configured

Created two Group Policy Objects and linked them to the **Marvel** OU:

1. An Avengers drive-mapping GPO for `\\DC01\AvengersShare`.
2. An X-Men drive-mapping GPO for `\\DC01\XMenShare`.

In each GPO, the drive mapping was configured under **User Configuration → Preferences → Windows Settings → Drive Maps**. The mapping used the **Update** action, a selected drive letter, a descriptive label, and **Reconnect**.

On each drive-map preference item's **Common** tab, I enabled **Run in logged-on user's security context** and **Item-level targeting**. The Avengers mapping targets users who are members of the **Avengers** security group; the X-Men mapping targets users who are members of the **X-Men** security group.

The GPOs remain in scope for users in the Marvel OU. Item-level targeting determines whether each individual drive-map preference is applied to a user.

## Validation

Refreshed Group Policy on the Windows 11 client and tested with two domain accounts:

- **Tony Stark**, a member of Avengers, received the Avengers share mapping only.
- **Scott Summers**, a member of X-Men, received the X-Men share mapping only.

Used `gpresult /r` to confirm both GPOs were applied to users in the Marvel OU. Both GPOs can appear in the report even when a user does not match one GPO's item-level targeting rule. Used `net use` on the client to inspect the current user's mapped network connections and UNC paths.

## Concepts demonstrated

- A **GPO** is a collection of user or computer configuration settings. Linking it to an OU defines where it is in scope.
- An **OU link** and a **security group** serve different purposes: the OU scopes the GPO; item-level targeting uses group membership to decide whether a specific drive-map item applies.
- A **UNC path** such as `\\DC01\XMenShare` is the network address used by clients. A local path such as `C:\ADLab\XMenShare` identifies the folder on the server itself.
- Mapping a drive and granting access are separate steps. **Share permissions** and **NTFS permissions** determine whether a user can open the files.
- **`gpresult /r`** reports applied GPOs; **`net use`** reports mapped network connections for the current user session.

## Related lab

See the [group-based file access lab](../ad-group-file-share-lab/README.md) for the OU, users, groups, shares, and permissions used here.
