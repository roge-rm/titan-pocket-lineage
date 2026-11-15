# LineageOS for the Unihertz Titan Pocket

An unofficial LineageOS 23 (Android 16) build for the Unihertz Titan Pocket. The source is in
`android_device_unihertz_titan_pocket` and `android_kernel_unihertz_mt6771` under this account.
This repo has the install steps, the update feed and the changelog, and the Releases have the
files.

No build is published yet. The first Release comes after the install and update tests on a phone
are done.

## What it runs on

- The Titan Pocket (MT6771, product name Titan_pocket), with the bootloader unlocked.
- Unihertz's May 2024 stock firmware, build Titan_pocket_20240514. If your phone has an older
  one, update it with Unihertz's updater first. Other firmware isn't supported, and the
  installer stops if it finds one.

## What you download

From the latest Release:

- `titan-pocket-installer-DATE.zip`, for the first install.
- `lineage-VERSION-DATE-UNOFFICIAL-titan_pocket.zip`, the update zip. You don't need it for
  the first install.
- `SHA256SUMS`, to check both files.

The zips have no Unihertz files in them. The installer makes the changes to the vendor
partition on your own phone, and the backup it makes is yours alone.

## Install

The install erases everything on the phone. Copy off what you want to keep first.

1. Unlock the bootloader if it isn't already (this erases the phone too).
2. Charge the phone to at least half.
3. On the computer you need Python 3.9 or later, Google's platform-tools (adb and fastboot)
   and about 10 GB free. Unzip the installer zip and put platform-tools in its folder, or on
   your PATH. On Windows you may need Google's USB driver.
4. Get Unihertz's May 2024 firmware zip (2024051420_g66v71c2k_dfl_tee.zip) from Unihertz. The
   installer only uses it if it has to put stock recovery back.
5. Start the phone in fastboot mode, or let the installer do it with `adb reboot bootloader`.
6. Run `./install.sh` on Linux, double-click `install.command` on macOS (right-click, Open,
   if macOS refuses) or `install.bat` on Windows.
7. It asks before each step that writes to the phone, and asks you to type "format" before
   it formats data. When our recovery starts, pick Advanced, then Enable ADB in its menu
   (volume keys move, power picks). The installer waits for that and goes on by itself.
8. It backs up your stock partitions into a `backups` folder next to the installer. That
   includes nvram, nvdata, nvcfg, protect1, protect2, persist and proinfo, which hold the
   phone's IMEI, Wi-Fi and Bluetooth addresses and calibration. They can't be rebuilt from
   anywhere else, so keep that folder somewhere safe.
9. It then writes the vendor changes, system and product, formats data, and writes boot and
   vbmeta. The phone restarts into LineageOS.

If you skip the format, the installer stops in our recovery and prints a `--finish` command.
Format data there (Factory reset, Format data/factory reset), go back to fastboot mode
(Advanced, Reboot to bootloader) and run that command. It writes boot and vbmeta.

## Updates

The Updater app (Settings, System, Updates) reads `updates/titan_pocket.json` in this repo and
downloads the update zip from the Release. Updates keep your apps and data. The Updater's own
setting for mobile data stays as shipped: it asks before downloading on a metered network.

Magisk and other root setups haven't been tested with updates yet.

## Go back to stock

The installer saved your stock partitions in its `backups` folder. With the phone in our
recovery and Advanced, Enable ADB picked, run from the installer folder:

    python3 tools/pocket-stock-restore.py BACKUP-FOLDER --serial SERIAL --stock-zip PATH/TO/2024051420_g66v71c2k_dfl_tee.zip

On Windows use `py -3` instead of `python3`. If adb and fastboot aren't on your PATH, add
`--adb platform-tools/adb --fastboot platform-tools/fastboot`. It writes the backup back and
leaves the phone in fastboot mode. Format data in stock recovery before starting stock.

If the installer stops part way, it prints what state the phone is in and the command that puts
stock back. To put only stock recovery back, with the phone in fastboot mode:

    python3 tools/pocket-install.py --put-back-recovery PATH/TO/2024051420_g66v71c2k_dfl_tee.zip

## Problems

Open an issue here. Say which Release you installed, whether it was the first install or an
update, what step it was at, and attach the installer's log file. The log is a `.log` file in
the `backups` folder, next to the backup subfolder it names. Attach only that file. Never share
the `backups` folder or anything in it except the log: it holds your IMEI, calibration data and
other private partitions.

## Licence

The build files here are Apache-2.0. LineageOS and Android have their own licences.
