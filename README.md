# Droidian for the Asus Zenfone Max Pro M2
A collection of tips to install and use Droidian on the Asus Zenfone Max Pro M2 (X01BD)
**NOTE:** This port is a work in progress! You can use it experience Droidian and play around with it, but that's all for now.

### Requirements
- A computer with fastboot and adb access to the phone
- Unlocked bootloader
- Backup all your data, as **your phone will be WIPED**

## Installation
### 0. Download files
- [Droidian `rootfs`](https://github.com/droidian-images/rootfs-api28gsi-all/releases/download/droidian%2Fbullseye%2F22/droidian-rootfs-api28gsi-arm64_20210531.zip) and [`devtools`](https://github.com/droidian-images/rootfs-api28gsi-all/releases/download/droidian%2Fbullseye%2F22/droidian-devtools-arm64_20210531.zip) for `arm64` (specific versions required)
- [Droidian adaptation](https://github.com/thomashastings/droidian-x01bd-guide/releases)
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
- Install zip file: `droidian-rootfs-api28gsi_arm64_20210531.zip` 
- Install zip file: `droidian-devtools_arm64_20210531.zip`
- Install zip file: `droidian-adaptation-x01bd_YYYYMMDD.zip`
- Go back to main menu and reboot to `System` (TWRP might complain that there is no OS installed, but that's fine)
- The first boot may take longer, and at least one spontaneous reboot is expected during the process
- If all goes well, your phone will boot to the Droidian lock screen, the unlock code is `1234`
- Flashing the `devtools` zip enables `SSH` over USB. To use it, connect your phone to your computer and type `ssh droidian@10.15.19.82`, the password is `1234` (on Windows, you may need [PuTTY](https://www.chiark.greenend.org.uk/~sgtatham/putty/))

## Notes
### Porting status
You can check out the status of the port [here](https://github.com/thomashastings/droidian-x01bd-guide/blob/main/STATUS.md).

## Credit
[aboothahir](https://gitlab.com/iAboothahir) (Zenfone Max Pro M1 port)

[kubersharma](https://sourceforge.net/u/kubersharma/profile/) (LineageOS)

[bauuuuu](https://forum.xda-developers.com/m/bauuuuu.6410262/) (LineageOS)

[Droidian](http://droidian.org/)

[Mobian](https://mobian-project.org/)

[UBports](https://ubuntu-touch.io/)


For further assistance, visit the [Droidian](https://t.me/droidianlinux) Telegram group.
