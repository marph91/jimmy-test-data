https://wiki.lineageos.org/devices/bramble/upgrade

Run `adb reboot sideload`.

*warning*

**Important:** The device may reboot to a blank black screen, fear not, this is a known bug on some recoveries, proceed with the instructions.

Run `adb sideload /path/to/zip` (inserting the path to your LineageOS package).

*check*

**Tip:** Normally, adb will report `Total xfer: 1.00x`, but in some cases, even if the process succeeds the output will stop at 47% and report `adb: failed to read command: Success`. In some cases it will report `adb: failed to read command: No error` or `adb: failed to read command: Undefined error: 0` which is also fine.

*(Optionally)*: If you want to install any add-ons, click `Advanced`, then `Reboot to Recovery`, then when your device reboots, click `Apply Update`, then `Apply from ADB`, then `adb sideload /path/to/zip` those packages in sequence.

*info\_outline*

**Note:** If you previously had any Google Apps add-on package installed on your device, you must install an updated package **before** the first boot of Android! If you did not have Google Apps installed, you must wipe the **Data** partition (or perform a factory reset) to install them.

*info\_outline*

**Note:** Add-ons aren’t signed with LineageOS’s official key, and therefore when they are sideloaded, Lineage Recovery will present a screen that says `Signature verification failed`, this is expected, please click `Continue`.

Once you have installed everything successfully, click the back arrow in the top left of the screen, then “Reboot system now”