# Enable Sidecar on Jailbroken iPhones (iOS 13.2+)

This guide helps you enable Sidecar on jailbroken iPhones running iOS 13.2 or higher.

## Introduction

Sidecar is disabled by default on iPhones, though the app still exists in the `/Applications/` folder. I discovered this when combing through the filesystem after the release of the checkra1n jailbreak. Curious, I edited the `Info.plist` file in `/Applications/Sidecar.app/`, enabling the app to appear on the home screen. To my surprise, it launched successfully. This led me to wonder why Apple disabled it on iPhones despite the technology being available. This project was born from that curiosity, along with a detailed guide for jailbroken users who wish to enable and use Sidecar on iPhones.

> **Note:**  
> This guide helps you disable the blacklist for iPhones in macOS. It requires edits to the root filesystem on your iPhone, so a jailbreak is necessary. Checkra1n is required.  
> Tested with macOS 10.15 (19A583) and iPhone 7 Plus (iOS 13.2.2).

---

## Patching Instructions - iPhone

> **Warning:**  
> This process is currently unstable with many known issues. **Use at your own risk.** Read through the known [Issues](#issues) before proceeding.

Assuming you're already jailbroken with checkra1n, follow these steps:

1. **Install Filza File Manager**  
   You can get Filza from Cydia or another repository for jailbroken devices.

2. **Install NewTerm 2**  
   This terminal app is required to run commands on your device.

3. **Navigate to `/Applications/Sidecar.app` in Filza**  
   Use Filza to browse the file system and find the `Sidecar.app` directory.

4. **Find and edit `Info.plist`**  
   Locate the `Info.plist` file in `/Applications/Sidecar.app/` and tap on it.

5. **Modify SBIconVisibilityDefaultVisable**  
   - Tap the ⓘ icon next to `SBIconVisibilityDefaultVisable`.
   - Toggle the switch to change the value from `NO` to `YES`.

6. **Exit the `Info.plist` file**  
   Tap the "< Info.plist" button in the upper-left corner to go back.

---

## Disabling System Integrity Protection (SIP) on macOS

Before proceeding with the macOS steps, you'll need to disable **System Integrity Protection (SIP)** on your Mac.

1. **Disable SIP**  
   - Reboot your Mac into Recovery Mode.
   - Open Terminal and run:  
     ```bash
     csrutil disable
     ```
   - Reboot into normal macOS.

2. **Verify SIP is Disabled**  
   Open Terminal and run:  
   ```bash
   csrutil status
   ```
   If SIP is disabled, the status will say "System Integrity Protection status: disabled."

---

## Patching macOS

1. **Clone the repository**  
   Open Terminal and clone the repository:
   ```bash
   git clone https://github.com/pookjw/SidecarPatcher
   ```

2. **Give execute permission**  
   Run the following command to grant execute permission:
   ```bash
   chmod +x SidecarPatcher/main.swift
   ```

3. **Run the patch script**  
   Use `sudo` to run the patch script:
   ```bash
   sudo swift SidecarPatcher/main.swift
   ```
   You'll be prompted to enter your macOS password.

> **Note:**  
> Ignore any warnings. If you encounter errors, upload the log to the [Issues page](https://github.com/pookjw/SidecarPatcher/issues). Please note that I may not respond to all issues.

The script will not re-patch your system unless you revert to the original `SidecarCore`.

---

## Known Issues

- **xcrun error** and **app crashes after rebooting**: Refer to [Issue #4](https://github.com/pookjw/SidecarPatcher/issues/4) for more details.
- **Other known issues**: Review the [Issues page](https://github.com/pookjw/SidecarPatcher/issues) for further information.

---

## Reverting the Patch

### Simple Method
1. Reinstall macOS using the Catalina Installer without erasing your disk. This will reinstall the system without deleting your data.

### Manual Method
1. **Disable SIP**  
   Follow the steps above to disable SIP on your Mac.

2. **Copy the original `SidecarCore`**  
   Run the following command:
   ```bash
   sudo cp /path/to/original/SidecarCore /System/Library/PrivateFrameworks/SidecarCore.framework/Versions/A/SidecarCore
   ```
   Replace `/path/to/original/SidecarCore` with the actual path to your backup of the original `SidecarCore`.

3. **Sign `SidecarCore`**  
   Run the following command to re-sign the framework:
   ```bash
   sudo codesign -f -s - /System/Library/PrivateFrameworks/SidecarCore.framework/Versions/A/SidecarCore
   ```

4. **Set permissions**  
   Set the correct permissions on the file:
   ```bash
   sudo chmod 755 /System/Library/PrivateFrameworks/SidecarCore.framework/Versions/A/SidecarCore
   ```

5. **Reboot**  
   After rebooting, you can re-enable SIP if desired by running:
   ```bash
   csrutil enable
   ```

---

## Conclusion

By following these steps, you should be able to enable Sidecar on your jailbroken iPhone. However, please remember that this method is experimental, and there may be issues. Always back up your device and proceed with caution.
