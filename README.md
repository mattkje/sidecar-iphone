Enables Sidecar on jailbroken iPhones running iOS 13.2 or higher.

Sidecar is disabled by default on iPhone by Apple, but still remains in the /Applications/ folder. I discovered this when combing through the filesystem shortly after the release of the checkra1n jailbreak. I figured I would head into /Applications/Sidecar.app/ and edit the Info.plist file, enabling the Sidecar app to show on the homescreen, allowing me to test if it would launch or not. Sure enough, it did. I was amazed and began wondering to myself why Apple would not allow Sidecar to run on the iPhone if the technology was there. That is what led to me deciding to make this project along with a guide for jailbroken users that explains, in detail, how to enable and make Sidecar function on the iPhone.

NOTE: This guide will help you disable the blacklist for iPhones in macOS. This also requires you to make some edits to the root filesystem on your iPhone, which requires a jailbreak. You will need to use checkra1n. Tested with macOS 10.15 (19A583) and iPhone 7 Plus (iOS 13.2.2).
Patching Instructions - iPhone

It is currently very unstable. There are many known issues. Read Issues. Please use this at your own risk. Assuming you're already jailbroken with checkra1n, follow the steps below.

1. Install Filza File Manager

2. Install NewTerm 2

3. Navigate to /Applications/Sidecar.app in Filza

4. Find the Info.plist file & tap on it

5. Click the ⓘ next to SBIconVisibilityDefaultVisable

6. Flip the switch on, which should change the value from NO to YES

7. Tap "< Info.plist" in the upper left corner.

System Integrity Protection. How to turn off System Integrity Protection on your Mac. After disabling System Integrity Protection, reboot into normal macOS.

    To check SIP is disabled: csrutil status

    Open Terminal application and clone this repository by running this command: git clone https://github.com/pookjw/SidecarPatcher

    Give excute permission: chmod +x SidecarPatcher/main.swift

    Run main.swift: sudo swift SidecarPatcher/main.swift

    You will need to enter your macOS password.

    Ignore warnings. If you encounter error and you don't know how to fix, upload a log to Issue. (I can't reply all issues because I don't know all.)

    This script will not patch again if you already patched your system until you revert to the original SidecarCore.

    About xcrun error and crashing many apps after rebooting: #4

How to revert

    Simplest Method

Reinstall your macOS using Catalina Installer. Install it without erasing your disk it won't erase your data and it will just reinstall the system.

    Using your backup

    Disable System Integrity Protection. How to turn off System Integrity Protection on your Mac.

To check SIP is disabled: csrutil status

    Run sudo mount -uw / command.

    Copy the original SidecarCore: sudo cp /path/to/original/SidecarCore /System/Library/PrivateFrameworks/SidecarCore.framework/Versions/A/SidecarCore

    Make sure you put the right path for SidecarCore /path/to/original/SidecarCore.

    Sign SidecarCore: sudo codesign -f -s - /System/Library/PrivateFrameworks/SidecarCore.framework/Versions/A/SidecarCore

    Set permission as 755: sudo chmod 755 /System/Library/PrivateFrameworks/SidecarCore.framework/Versions/A/SidecarCore

    Reboot. If you want to enable System Integrity Protection again, you can do so now.
