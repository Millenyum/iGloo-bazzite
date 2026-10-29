Third alpha of iGloo: migrate from Windows 11 to Linux without touching a terminal.

Validated end-to-end on bare metal, dual-boot alongside Windows 11:

- Fedora KDE
- Linux Mint Cinnamon
- Debian (GNOME)

New and **experimental** (not yet validated on hardware):

- Bazzite DX

## Added

- Bazzite DX, Universal Blue's gaming system with developer tools (VS Code, Docker and Podman, distrobox, libvirt, Homebrew). iGloo installs it unattended from the Fedora netinstall and downloads the system image during the install. NVIDIA machines get the NVIDIA edition, so the first session already runs on the right driver. Updates are checked against Universal Blue's signature. The user logs in to the Plasma desktop with their password, instead of Bazzite DX's default passwordless start into Steam Gaming Mode. Firefox and Bazzite's other default apps are installed at first boot, and files, browsers, Wi-Fi and display settings are migrated as on the other distributions.
- With Secure Boot on, the pre-flight check explains the one-time key confirmation Bazzite needs at the first reboot.

## Fixed

- The test `blkid` stub is created owner-only instead of world-executable.

The full list is in the [changelog](https://github.com/Millenyum/iGloo-bazzite/blob/main/CHANGELOG.md).

## Known limitations

- Fedora: the KDE first-login setup screen still appears once ([#1](https://github.com/gillesduif/iGloo/issues/1))
- Mint: wallpaper scaling on landscape monitors uses zoom instead of fit ([#2](https://github.com/gillesduif/iGloo/issues/2))
- Debian: creates a second 1 GB EFI partition instead of reusing the Windows one ([#227](https://github.com/gillesduif/iGloo/issues/227))
- The boot menu labels the Windows entry "Windows 11" on Windows 10 machines ([#228](https://github.com/gillesduif/iGloo/issues/228))
- Boot can take around 100 seconds between the menu and the login screen on NVMe ([#221](https://github.com/gillesduif/iGloo/issues/221))
- Locales without a glibc equivalent, such as en-BE, fall back rather than map ([#220](https://github.com/gillesduif/iGloo/issues/220))
- Bazzite DX is experimental: it has not been installed on physical hardware yet. It needs a network connection during the install, and NVIDIA cards older than the GTX 16-series are not supported by the image it picks for them.
- Unsigned installer: SmartScreen will warn (click "More info" > "Run anyway")

SHA256 of `iGloo-Setup-0.3-alpha.exe`:

```
<SHA256 printed by installer\build-setup.bat>
```

Requires Windows 10 (version 1809) or Windows 11. On systems with an NVIDIA GPU and Secure Boot enabled, the installation completes but the locally compiled NVIDIA module is rejected by the kernel; the pre-flight check warns about this in advance. Linux Mint is the exception: it ships pre-signed NVIDIA modules and works with Secure Boot enabled. Read the [README](https://github.com/gillesduif/iGloo#readme) for the full safety model before running.
