# Group Policy Lab — DC OU Wallpaper Deployment

## Objective
Centrally deploy a desktop wallpaper to users in the DC organizational unit using Group Policy and an SMB network share.

## Environment
- DC01: Windows Server domain controller and SMB file server
- Domain-joined Windows 11 VM
- DC OU and test account: Bruce Wayne
- Image stored locally at `C:\ADLab\DCWallpaper\batman.jpg`

## Configuration
1. Prepared a JPG image on DC01.
2. Shared the wallpaper folder with the share name **DC Wallpaper**.
3. Configured read-only share access for domain users.
4. Checked NTFS permissions to allow domain users to read the image without granting unnecessary write access.
5. Created the GPO `DC - Desktop Wallpaper` and linked it to the DC OU.
6. Enabled **User Configuration > Policies > Administrative Templates > Desktop > Desktop > Desktop Wallpaper**.
7. Set the wallpaper path to:

   ```text
   \\DC01\DC Wallpaper\batman.jpg
   ```

8. Selected **Fill** for wallpaper style.
9. Signed into Windows 11 as Bruce Wayne, refreshed policy with `gpupdate /force`, and signed out and back in.

## Result
**Passed:** Batman wallpaper appeared automatically for Bruce Wayne on the domain-joined Windows 11 workstation. The user also reported completing a `gpresult /r` check.

## Concepts practiced
- Centralized desktop configuration using Group Policy
- SMB sharing and UNC paths
- Share permissions vs. NTFS permissions
- Implicit vs. explicit deny
- Least-privilege read access
- User policy refresh and logon testing

## Operational note
For production use, store shared wallpaper assets on a properly managed file share, ensure all targeted clients can reach the UNC path, and avoid granting write permissions to ordinary users.
