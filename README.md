# PixelOS 17 for Motorola One Vision (kane)

Unofficial PixelOS builds for the Motorola One Vision (kane).

PixelOS is an AOSP-based custom ROM that brings the Pixel look and features, with Google apps included. These builds are based on PixelOS 17 (Android 17) and the LineageOS 24 device sources for kane.

| | |
|---|---|
| **Device** | Motorola One Vision (kane): XT1970-1, XT1970-2, XT1970-3 |
| **Android** | 17 |
| **Kernel** | Linux 4.14 |
| **Based on** | PixelOS 17 / LineageOS 24 |
| **Build type** | user, signed with private release keys |
| **Status** | Beta |
| **Maintainer** | [luizpaulo2005](https://github.com/luizpaulo2005) |

## Downloads

- **ROM zip:** [SourceForge](https://sourceforge.net/projects/pixelos-kane/files/). The zip is larger than GitHub's 2 GiB limit.
- **Fastboot images and source manifest:** [GitHub Releases](https://github.com/luizpaulo2005/pixelos-kane/releases)
- **Support and discussion:** [XDA thread](https://xdaforums.com/t/rom-17-unofficial-pixelos-17-for-motorola-one-vision-kane.4806593/)

| File | Use |
|---|---|
| `boot.img` | Kernel and recovery |
| `dtbo.img` | Device tree overlay |
| `vbmeta.img` | Verified boot metadata |
| `super_empty.img` | Super partition layout (`fastboot wipe-super`) |
| `build-manifest.xml` | Exact commit of every repository in the build |

## What works

- Boot, SELinux Enforcing, encryption
- RIL: calls, SMS, mobile data
- VoLTE (HD calls) and Wi-Fi calling, tested on Vivo (Brazil)
- Wi-Fi (including WPA3 networks), hotspot (WPA2/WPA3), Bluetooth
- Camera (rear, front, flash), video recording
- Fingerprint
- Audio, microphone, vibration
- GPS and sensors
- Moto gestures (chop-chop flashlight fixed in these builds)
- Google apps and Play Store
- Banking apps tested: Banco do Brasil, Nubank

## Known issues

- Play Integrity: only `MEETS_BASIC_INTEGRITY` passes (DEVICE and STRONG fail, as expected with an unlocked bootloader).
- Right after turning Wi-Fi off, a call may fall back to 3G until IMS re-registers over LTE (about a minute).
- Hotspot in WPA3-only mode: clients cannot connect. Use the default WPA2/WPA3 mode.

Please report other issues with logs.

## Installation

Clean install from stock, LineageOS or any other ROM. Your bootloader must be unlocked. **This wipes all your data.**

1. Download the zip and `boot.img`, `dtbo.img`, `vbmeta.img`, `super_empty.img`.
2. Reboot to bootloader (power off, hold Volume Down + Power).
3. Flash the partitions:
   ```
   fastboot flash vbmeta vbmeta.img
   fastboot flash dtbo dtbo.img
   fastboot wipe-super super_empty.img
   fastboot flash boot boot.img
   ```
4. Using the volume keys, choose **Recovery Mode** and confirm with Power.
5. In recovery: **Factory reset > Format data / factory reset**.
6. **Apply update > Apply from ADB**, then on your computer:
   ```
   adb sideload PixelOS_kane-17.0-<date>-UNOFFICIAL-signed.zip
   ```
7. **Reboot system now.** The first boot takes 5 to 10 minutes.

## Updating

From a previous build of this ROM: Recovery > **Apply update > Apply from ADB** > `adb sideload` the new zip > Reboot. No wipe needed.

## Changes in these builds

- System, system_ext, product and vendor use EROFS (lz4hc), so Google apps fit in the super partition.
- Fixed the chop-chop flashlight gesture (MotoActions), also [sent to LineageOS](https://review.lineageos.org/c/LineageOS/android_hardware_motorola/+/510602).
- Signed with private release keys.

## Sources

- Device tree: [luizpaulo2005/android_device_motorola_kane](https://github.com/luizpaulo2005/android_device_motorola_kane/tree/lineage-24.0)
- Common tree: [luizpaulo2005/android_device_motorola_exynos9610-common](https://github.com/luizpaulo2005/android_device_motorola_exynos9610-common/tree/lineage-24.0)
- Kernel: [LineageOS/android_kernel_motorola_exynos9610](https://github.com/LineageOS/android_kernel_motorola_exynos9610/tree/lineage-24.0)
- Motorola hardware: [luizpaulo2005/android_hardware_motorola](https://github.com/luizpaulo2005/android_hardware_motorola/tree/lineage-24.0)
- Local manifest: [luizpaulo2005/local_manifests_kane](https://github.com/luizpaulo2005/local_manifests_kane)
- PixelOS: [PixelOS-AOSP](https://github.com/PixelOS-AOSP)

## Credits

- PixelOS team
- LineageOS and the kane maintainers (Stricted, npjohnson, DaemonMCR)
- TheMuppets for the proprietary blobs
