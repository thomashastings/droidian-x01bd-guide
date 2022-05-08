# Droidian for the Asus Zenfone Max Pro M2
A collection of tips to install and use Droidian on the Asus Zenfone Max Pro M2 (X01BD)
**NOTE:** This port is work in progress! You can use it experience Droidian and play around with it, but that's all for now.

### Requirements
- A computer with fastboot and adb access to the phone
- Unlocked bootloader
- Backup all your data, as **your phone will be WIPED**
- It is also recommended to take a note about your `Acces Point Name` in Android `Settings` before starting the procedure (you may need it to configure mobile data)

## Installation
### 0. Download files
- [Droidian `rootfs` and `devtools`](https://github.com/droidian-images/rootfs-api28gsi-all/releases) for `arm64` (nightly releases include devtools)
- [Android 9 Pie Firmware](https://dlcdnets.asus.com/pub/ASUS/ZenFone/ZB631KL/UL-ASUS_X01BD-WW-16.2017.1912.072.999-user.zip)
- [Lineage OS 16](https://sourceforge.net/projects/kubersharma001/files/X01BD/lineage-16.0/lineage-16.0-20191119-UNOFFICIAL-X01BD.zip/download) (unofficial build)
- Latest [TWRP](https://dl.twrp.me/X01BD/)

### 1. Install TWRP 
- Boot to fastboot mode by pressing the Vol+ and Power buttons until the phone vibrates
- Check that the phone is recognized by running `fastboot devices`
- Install TWRP by running `fastboot flash recovery twrp-*-X01BD.img`

### 2. Install Droidian in TWRP
TWRP:
- Boot into TWRP by pressing Vol- and Power buttons until the phone vibrates
- Go to `Wipe` and `Format data` (type yes)
- IMPORTANT: **Reboot into TWRP again**

PC:
- Connect the phone via USB
- The internal storage is now available over MTP from the PC
- Copy the downloaded files to the internal storage of the phone

TWRP:
- Install zip file: `UL-ASUS_X01BD-WW-16.2017.1912.072.999-user.zip`
- Install zip file: `lineage-16.0-20191119-UNOFFICIAL-X01BD.zip`
- Install zip file: `droidian-rootfs-api28gsi_arm64_YYYYMMDD.zip` 
- Install zip file: `droidian-devtools_arm64_YYYYMMDD.zip` (this is included in nightly releases)
- Go back to main menu and reboot to `System` (TWRP might complain that there is no OS installed, but that's fine)
- The first boot may take longer, and at least one spontaneous reboot is expected during the process
- If all goes well, your phone will boot to the Droidian lock screen, the unlock code is `1234`
- Flashing the `devtools` zip enables `SSH` over USB. To use it, connect your phone to your computer and type `ssh droidian@10.15.19.82`, the password is `1234` (on Windows, you may need [PuTTY](https://www.chiark.greenend.org.uk/~sgtatham/putty/))

## Notes
### Porting status
You can check out the status of the port [here](https://github.com/thomashastings/droidian-x01bd-guide/blob/main/STATUS.md).

### Applications
You can find a list of mobile-friendly Linux applications at [LinuxPhoneApps](https://linuxphoneapps.org/).

### Mobile data
Mobile data should work, but some manual setup may be required. The good part is that the configuration is persistent, so you need to do this only once.
- Open the `Settings` app and tap `Mobile`, then tap `Access Point Names`
- Tap the `+` in the top right corner of the pop-up
- Fill out the textboxes based on your settings in Android. The `Name` can be anything, e. g., the name of your carrier. The `APN` is likely some sort of an URL, like `internet.carrier.net` or something similar. If you didn't see a `Username` and `Password` in Android, you can skip these. 

In some cases, rebooting your phone or turning mobile data on and off a few times is enough.
Otherwise we'll have to give the same settings to [oFono](https://en.wikipedia.org/wiki/OFono) as well.
- Open the `King's Cross` terminal app or use `SSH` and type `cd /usr/share/ofono/scripts`
- To check your current setup, type `./list-contexts`, look for the first context, called `[ /ril_1/context1 ]`
- Notice that context has `Name`, `Type`, `AccessPointName`, `Username`, and `Password` attributes among others, we'll need to change these to match the valid settings from Android. 
- Now deactivate this context to be able to make changes to it: `./deactivate-context 1`
- And now make your changes like this: `./set-context-property 1 $ATTRIBUTE $VALUE`, where the `1` is for `[ /ril_1/context1 ]`, the `$ATTRIBUTE` is one of the attributes listed above, and the `$VALUE` will be the value you need to enter. make sure that the `Name` and `AccessPointName` match the `Name` and `APN` you entered in the settings menu. If an attribute needs to be empty, set it to `""`.
- When you make your changes, you can use `./list-contexts` to see them.
- When everything looks good, activate the updated context: `./activate-context 1` 
- If all went well, by running`./list-contexts` again you should see that the `Active` attribute is now `1`, and under the `Settings` attribute you can see the network parameters (Address, Netmask, Gateway, etc.) assigned by your carrier.
- You may need to reboot or turn mobile data on and off a few times, but mobile data should be working now.

- Pro tip: once you configured everything, you can type `history` to see your previous commands. Save them to a script that does all of this for you next time.


## Credit
[aboothahir](https://gitlab.com/iAboothahir) (Zenfone Max Pro M1 port)

[kubersharma](https://sourceforge.net/u/kubersharma/profile/) (LineageOS)

[bauuuuu](https://forum.xda-developers.com/m/bauuuuu.6410262/) (LineageOS)

[Droidian](http://droidian.org/)

[Mobian](https://mobian-project.org/)

[UBports](https://ubuntu-touch.io/)


For further assistance, visit the [Droidian](https://t.me/droidianlinux) Telegram group.
