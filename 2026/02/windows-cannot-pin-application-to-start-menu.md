# Windows Cannot Add Application to Start Menu

## Problem Description

In the Windows system, when you press the Win key to open the Start Menu, you may sometimes fail to pin the Thunderbird application to the top "Pinned" section. This occurs because if the "Add to Start Menu" option was not selected during Thunderbird installation, the system will not recognize it as a pinnable application. Consequently, directly performing the "Pin to Start" action on `thunderbird.exe` will be ineffective.

## Solution

1.  **Open the Start Menu Programs Directory**
    In File Explorer's address bar, enter the following path and press Enter:
    `%ProgramData%\Microsoft\Windows\Start Menu\Programs`

2.  **Place the Thunderbird Shortcut**
    Copy or drag Thunderbird's shortcut file (`.lnk` file) into this directory.

3.  **Perform the Pinning Operation**
    Return to the Start Menu, locate the newly added Thunderbird shortcut, right-click on it, and select **"Pin to Start"**.

After completing these steps, the Thunderbird icon will appear correctly in the pinned section at the top of the Start Menu, allowing for quick access via the Win key.
