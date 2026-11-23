# Changelog

Newest first. Each entry is a Release with an installer zip and an update zip.

<!-- new entries go here -->

## lineage-23.2-20261123-015625 (2026-11-23)

- LineageOS 23.2, Android 16, security patch 2026-11-01.
- Needs Unihertz stock Titan_pocket_20240514 to install.
- Battery gauge uses an OCV table measured on this phone, so the percentage is right down to empty
- Vendor overlay v14: fewer SELinux denials at boot
- Magisk users can keep root through updates: run `su -c pocket-magisk-stash enable` once, and each update the Updater downloads gets a patched boot ready for recovery
- PIN entry on the lock screen works with the hardware keyboard
- LineageOS 23.2 with the November 2026 security patches
- Calls and the modem don't work yet
