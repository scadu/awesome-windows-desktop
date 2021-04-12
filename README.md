# zomg-windows-desktop

## What's that?
This repository contains information regarding my Windows setup and some scripts and utils in use.
___
### Preparation
#### Enable symlink support for standard (non-administrator) accounts
You can do it by enabling [Developer Mode](https://docs.microsoft.com/en-us/windows/apps/get-started/enable-your-device-for-development), or [updating the Local Security Policy](#local-security-policy).

###### Local Security Policy
Open `Local Security Policy` (`secpol.msc`) and go to `Local Policies` -> `User Rights Assignment`, select `Create symbolic links`, add your user to the list and **reboot**.

> I haven't found a reliable way to automate it.
> It's possible to export Local Security Policy to a file, edit the file and import back but I'm not convinced of this method.

#### Enable long paths
More information can be found in [Microsoft docs](https://docs.microsoft.com/en-us/windows/win32/fileio/maximum-file-path-limitation#enable-long-paths-in-windows-10-version-1607-and-later).

You can enable long path support editing the registry key or administrative template in the Group Policy that controls this registry key.
##### Registry key
> Run as administrator

`Set-ItemProperty 'HKLM:\System\CurrentControlSet\Control\FileSystem' -Name 'LongPathsEnabled' -value 1`

##### Group policy
`Computer Configuration > Administrative Templates > System > Filesystem > Enable Win32 long paths`.
___

### Caveats

#### High DPI
[Windows scaling issues](https://support.microsoft.com/en-us/topic/windows-scaling-issues-for-high-dpi-devices-508483cd-7c59-0d08-12b0-960b99aa347d)

[Fix apps that appear blurry in Windows 10](https://support.microsoft.com/en-us/windows/fix-apps-that-appear-blurry-in-windows-10-e9fe34ab-e7e7-bc6f-6695-cb169b51de0f)

[Make older apps or programs compatible with Windows 10](https://support.microsoft.com/en-us/windows/make-older-apps-or-programs-compatible-with-windows-10-783d6dd7-b439-bdb0-0490-54eea0f45938)

For some reason, the trick with compatibility mode works for [PatchMyPC](https://patchmypc.com/home-updater) (which is DPI-unaware), when setting `Application` in the `Override high DPI scaling behavior`.
___

### Do not allow pplications from taking exclusive control of sound adapter
There are cases when applications takes control over sound adapter adjusting volume level automatically messing with our settings. Also, it means that only one application at a time can use your audio interface.

To prevent such behavior open `Control Panel` and go to `Sound` section, select your device and from `Advanced` tab uncheck `Allow applications to take exclusive control of this device` checkbox.