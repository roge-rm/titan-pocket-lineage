# Changelog

Newest first. Each entry is a Release with an installer zip and an update zip.

<!-- new entries go here -->

## lineage-23.2-20261126-223603 (2026-11-26)

- LineageOS 23.2, Android 16, security patch 2026-11-01.
- Needs Unihertz stock Titan_pocket_20240514 to install.
- microSD cards work (exFAT tested, FAT32 not tested yet)
- File transfer over USB works with USB debugging on
- Fixed reboots under heavy load, like restoring a large SMS backup
- Fixed a crash under memory pressure, and zram swap is on
- Keyboard: Alt is a plain modifier (tap for sticky Alt), Sym opens the symbols page, holding Shift turns caps lock on or off
- Touchpad: Keyboard swipes can move the text cursor (Pocket Keyboard settings)
- Pocket Rotation: choose how apps may rotate the screen
- Aperture: the preview fills the square screen, smaller controls and a 1:1 photo ratio
- Full-size 16 MP photos and RAW on the main camera for camera apps that ask for them
- The screen lights up briefly for new notifications
- Magisk root keeper shows a notification while it prepares the patched boot and when it's ready
- Fewer Bluetooth stack restarts from stray advertising replies
- A hung phone now reboots by itself and leaves a log
- Installing a second local update in one go: if no install prompt shows, force stop the Updater and try again

## lineage-23.2-20261123-015625 (2026-11-23)

- LineageOS 23.2, Android 16, security patch 2026-11-01.
- Needs Unihertz stock Titan_pocket_20240514 to install.
- Battery gauge uses an OCV table measured on this phone, so the percentage is right down to empty
- Vendor overlay v14: fewer SELinux denials at boot
- Magisk users can keep root through updates: run `su -c pocket-magisk-stash enable` once, and each update the Updater downloads gets a patched boot ready for recovery
- PIN entry on the lock screen works with the hardware keyboard
- LineageOS 23.2 with the November 2026 security patches
- Calls and the modem don't work yet
