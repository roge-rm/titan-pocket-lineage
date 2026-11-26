# LineageOS for the Unihertz Titan Pocket

An unofficial LineageOS 23 (Android 16) build for the Unihertz Titan Pocket. It runs on a 5.10 kernel. The source is in [android_device_unihertz_titan_pocket](https://github.com/roge-rm/android_device_unihertz_titan_pocket) and [android_kernel_unihertz_mt6771](https://github.com/roge-rm/android_kernel_unihertz_mt6771). Download the files from the [Releases](https://github.com/roge-rm/titan-pocket-lineage/releases).

## What works

Tested on my own phone. So far it has only been tested with Fido in Canada.

| Feature | Status |
|---|---|
| Calls and VoLTE, both SIM slots, SIM swap | Works |
| SMS | Works |
| Mobile data | Works, off by default |
| Wi-Fi | Works |
| Bluetooth, music and calls | Works |
| GPS | Works |
| Front and rear camera, flash, 1080p video | Works |
| Flashlight | Works |
| Fingerprint (front strip) | Works |
| Speaker, mic and headphones | Works |
| FM radio | Works, needs headphones |
| Keyboard, keyboard light and touchpad | Works |
| Charging, also with the phone off | Works |
| Sleep | Works |
| USB (adb, file transfer) | Works |
| microSD | Works with exFAT cards, FAT32 not tested yet |
| Encryption, SELinux enforcing | Works |
| Updates through the Updater | Works |
| IR blaster | LED lights up, not tried on a TV yet |
| Notification light | Not tested |
| MMS, hotspot, Wi-Fi calling, NFC, USB OTG | Not tested |

Added on top of LineageOS:

| Feature | What it does |
|---|---|
| Pocket Keyboard app | Keyboard light timeout, touchpad swipes to scroll or move the text cursor, Alt+B/C/S shortcuts, FUNC1 and FUNC2 press and long press actions |
| Display modes | Stock's portrait mini mode, square zoom-out modes in several sizes and a custom size. Quick Settings tile, hold FUNC1 and FUNC2 for a second to go back to normal |
| Pocket Rotation app | Choose how apps may rotate the screen |
| Camera on the square screen | Aperture's preview fills the screen, with a 1:1 photo ratio |
| Charging control | Settings, Battery |
| Front strip | Tap for Home |
| Lock screen | Type your PIN on the keyboard |
| Root through updates | Keeps Magisk root after an update (see Updates) |

Let me know what works and what doesn't by opening an issue here.

## What it runs on

- The Titan Pocket (MT6771, product name Titan_pocket), with the bootloader unlocked.
- Unihertz's May 2024 stock firmware, build Titan_pocket_20240514. If your phone is on an older one, update it with Unihertz's updater first. The installer stops if it finds any other firmware.

## What to download

From the latest Release:

- `titan-pocket-installer-DATE.zip`, for the first install.
- `lineage-VERSION-DATE-UNOFFICIAL-titan_pocket.zip`, the update zip. You don't need it for the first install.
- `SHA256SUMS`, to check both files.

No Unihertz files are in the zips. The installer makes the vendor changes on your own phone, and the backup it makes stays with you.

## Install

The install erases everything on the phone. Copy off what you want to keep first.

1. Unlock the bootloader if it isn't already (this erases the phone too).
2. Charge the phone to at least half.
3. On the computer you need Python 3.9 or later, Google's platform-tools (adb and fastboot) and about 10 GB free. Unzip the installer zip and put platform-tools in its folder, or on your PATH. On Windows you may need Google's USB driver.
4. Get Unihertz's May 2024 firmware zip (2024051420_g66v71c2k_dfl_tee.zip) from Unihertz. The installer only uses it if it has to put stock recovery back.
5. Start the phone in fastboot mode, or let the installer do it with `adb reboot bootloader`.
6. Run `./install.sh` on Linux, double-click `install.command` on macOS (right-click, Open, if macOS refuses) or run `install.bat` on Windows.
7. The installer asks before each step that writes to the phone. Type "format" when it asks, before it formats data.
8. When our recovery starts, pick Advanced, then Enable ADB (volume keys move, power picks). The installer waits for that and carries on by itself.
9. It backs up your stock partitions into a `backups` folder next to the installer. Keep that folder somewhere safe. It holds nvram, nvdata, nvcfg, protect1, protect2, persist and proinfo. Those have the phone's IMEI, Wi-Fi and Bluetooth addresses and calibration, and they can't be rebuilt from anywhere else.
10. It writes the vendor changes, system and product, formats data, then writes boot and vbmeta. The phone restarts into LineageOS.

If you skip the format, the installer stops in our recovery and prints a `--finish` command. Format data there (Factory reset, Format data/factory reset). Go back to fastboot mode (Advanced, Reboot to bootloader) and run that command. It writes boot and vbmeta.

## Updates

The Updater app (Settings, System, Updates) checks `updates/titan_pocket.json` here and downloads the update zip from the Release. Updates keep your apps and data. On a metered network the Updater asks before downloading.

If you use Magisk, run this once to keep root through updates:

    su -c pocket-magisk-stash enable

After that, each update the Updater downloads gets a Magisk patched boot ready, and recovery writes it after the update. `su -c pocket-magisk-stash status` shows what's ready. `su -c pocket-magisk-stash disable` turns it off. It needs Magisk 28 or newer. A notification says when the Magisk patched boot is ready. Tap Install after it says "Root is ready for the update".

## Go back to stock

The installer saved your stock partitions in its `backups` folder. Start the phone in our recovery, pick Advanced, then Enable ADB, and run this from the installer folder:

    python3 tools/pocket-stock-restore.py BACKUP-FOLDER --serial SERIAL --stock-zip PATH/TO/2024051420_g66v71c2k_dfl_tee.zip

On Windows use `py -3` instead of `python3`. If adb and fastboot aren't on your PATH, add `--adb platform-tools/adb --fastboot platform-tools/fastboot`. It writes the backup back and leaves the phone in fastboot mode. Format data in stock recovery before you start stock.

If the installer stops part way, it prints what state the phone is in and the command that puts stock back. To put only stock recovery back, with the phone in fastboot mode:

    python3 tools/pocket-install.py --put-back-recovery PATH/TO/2024051420_g66v71c2k_dfl_tee.zip

## Problems

Open an issue here. Say which Release you installed, whether it was the first install or an update and what step it was at. Attach the installer's log, the `.log` file in the `backups` folder next to the backup subfolder it names.

Attach only the log. Never share the rest of the `backups` folder - it holds your IMEI, calibration data and other private partitions.

## Licence

The build files here are Apache-2.0. LineageOS and Android have their own licences.
