# 🔧 TWRP Recovery for TECNO Camon 30S (CLA5)
Unofficial **TWRP Recovery** port for the **TECNO Camon 30S (CLA5)**.
This project is currently under development.
---
# 📱 Device
- **Device:** TECNO Camon 30S
- **Codename:** CLA5
- **Android:** Android 15
- **Platform:** MediaTek
- **Recovery:** TWRP
- **Status:** 🟡 Work in Progress
---
# ⚙️ Current Status
TWRP successfully boots on the **TECNO Camon 30S (CLA5)**.
However, there is currently a major problem:
> ❌ **The touchscreen does not respond in TWRP Recovery.**
The display works and TWRP starts, but touch input is not detected.
The touchscreen works correctly in the normal Android system.
This means that the touchscreen hardware itself appears to be functional.
---
# 🖥️ TWRP
Current status:
| Component | Status |
|-----------|--------|
| TWRP boots | ✅ Working |
| Display | ✅ Working |
| Touchscreen | ❌ Not working |
| Buttons | 🟡 Testing |
| ADB | 🟡 Testing |
| MTP | 🟡 Testing |
| USB OTG | 🟡 Testing |
| Vibration | 🟡 Testing |
| Decryption | 🟡 Testing |
| Backup / Restore | 🟡 Testing |
| Flashing ZIP files | 🟡 Testing |
---
# 🖐️ Touchscreen Problem
The touchscreen appears to use a **FocalTech controller**.
The issue may be related to:
- FocalTech touchscreen driver;
- Touchscreen firmware loading;
- `vendor_boot.img`;
- DTB / DTBO;
- TWRP device tree configuration;
- Kernel touchscreen driver;
- Touchscreen initialization during recovery boot.
---
# 📦 Touchscreen Firmware
The required touchscreen firmware files are already present in the recovery environment:
```text
recovery/vendor/firmware/focaltech_ts_fw.bin
recovery/vendor/firmware/fs1599.fsm
```
The files are included, but simply copying the firmware into the recovery image does not make the touchscreen work.
This suggests that the problem may not be the firmware files themselves.
The touchscreen driver may not be loading or initializing correctly.
---
# 🔍 What Needs to Be Investigated
The main goal is to determine why the **FocalTech touchscreen driver is not being initialized correctly in TWRP**.
Possible areas that may need to be checked:
```text
vendor_boot.img
DTB
DTBO
vendor/firmware
TWRP device tree
Kernel touchscreen driver
ueventd.rc
init*.rc
```
It may be necessary to compare the stock Android / recovery environment with the TWRP environment to determine which files, permissions, properties, services, drivers, or configurations are missing.
---
# 🧪 Stock Android
The touchscreen works correctly in the normal Android system.
This is important because it indicates that the touchscreen hardware itself is most likely working correctly.
The problem only appears when booting into **TWRP Recovery**.
Therefore, the issue is most likely related to:
- Recovery kernel;
- FocalTech driver;
- Firmware loading;
- Device Tree;
- DTBO;
- GPIO configuration;
- I2C configuration;
- IRQ configuration;
- Regulator / power configuration;
- Recovery `init` scripts;
- `ueventd.rc`;
- Vendor configuration;
- TWRP device tree;
- Missing libraries or services.
---
# 🔬 Possible Causes
The touchscreen may require additional components from the stock firmware.
Possible missing components include:
- Touchscreen kernel driver;
- FocalTech firmware;
- Device Tree configuration;
- DTBO configuration;
- GPIO configuration;
- I2C configuration;
- Interrupt / IRQ configuration;
- Power / regulator configuration;
- Initialization scripts;
- Required permissions;
- Required vendor libraries;
- Required vendor services;
- Kernel modules;
- Touchscreen configuration files.
Further investigation is required to determine exactly which component is missing from the TWRP environment.
---
# 🧩 Recovery Environment
Current recovery structure:
```text
recovery/
└── vendor/
    └── firmware/
        ├── focaltech_ts_fw.bin
        └── fs1599.fsm
```
The firmware files are present, but the touchscreen driver still does not initialize correctly.
---
# 🛠️ Possible Things to Check
The following areas should be compared between the stock Android environment and TWRP:
```text
/vendor/firmware
/vendor/etc
/vendor/lib
/vendor/lib64
/vendor/bin
/vendor/etc/init
/vendor/etc/ueventd.rc
/system/etc
/proc/device-tree
/sys/class/input
/sys/bus/i2c
/sys/class/gpio
```
The kernel logs should also be checked for FocalTech-related messages.
For example:
```bash
dmesg | grep -i focal
```
```bash
dmesg | grep -i touch
```
```bash
dmesg | grep -i touchscreen
```
```bash
dmesg | grep -i i2c
```
```bash
dmesg | grep -i firmware
```
It may also be useful to check available input devices:
```bash
cat /proc/bus/input/devices
```
and:
```bash
ls -la /dev/input/
```
---
# 🧬 Device Tree / DTBO
The touchscreen configuration may be located in the Device Tree.
Important areas to investigate include:
```text
DTB
DTBO
I2C
GPIO
IRQ
Regulators
Power supplies
Pin control
Touchscreen nodes
```
The stock DTB/DTBO should be compared with the TWRP environment.
A missing or incorrect touchscreen node could prevent the FocalTech driver from initializing.
---
# 🐧 Kernel
The recovery kernel may require the correct FocalTech touchscreen driver.
The following should be checked:
```text
FocalTech driver
I2C touchscreen driver
Kernel modules
Firmware loader
Input subsystem
GPIO
IRQ
Regulator support
```
If the required driver is missing from the recovery kernel, simply copying the firmware files will not be enough.
---
# 📜 Init / ueventd
The following files may also need to be checked:
```text
init*.rc
ueventd.rc
```
Possible problems include:
- Missing initialization commands;
- Incorrect permissions;
- Missing device nodes;
- Missing firmware paths;
- Missing properties;
- Missing services;
- Missing vendor initialization scripts.
---
# 🧪 Debugging
Useful logs from TWRP would be:
```bash
dmesg
```
```bash
logcat
```
```bash
cat /proc/bus/input/devices
```
```bash
getevent -lp
```
```bash
ls -la /dev/input/
```
```bash
find /sys -iname "*touch*" 2>/dev/null
```
These logs can help determine whether the touchscreen driver is loaded and whether an input device is created.
---
# 📥 Information Available
The following files/information can be provided for debugging:
```text
vendor_boot.img
boot.img
DTB
DTBO
stock recovery
TWRP recovery image
kernel information
dmesg
logcat
/proc/bus/input/devices
getevent -lp
```
---
# 🆘 Help Needed
If you have experience with:
- **TWRP**
- **MediaTek**
- **FocalTech Touchscreen**
- **Android Recovery**
- **vendor_boot**
- **DTB / DTBO**
- **Linux Kernel**
- **Android Device Trees**
- **Android Input Subsystem**
please help me determine why the touchscreen does not work in TWRP.
I would especially appreciate help identifying:
- Which touchscreen driver is required;
- Which FocalTech firmware files need to be loaded;
- Whether additional files need to be copied from the stock firmware;
- Whether `init*.rc` needs to be modified;
- Whether `ueventd.rc` needs to be modified;
- Whether DTB changes are required;
- Whether DTBO changes are required;
- Whether GPIO configuration needs to be changed;
- Whether I2C configuration needs to be changed;
- Whether IRQ configuration needs to be changed;
- Whether regulator / power configuration needs to be changed;
- Whether kernel modules are required;
- Whether additional vendor libraries are required;
- Whether additional vendor services are required;
- Whether the TWRP device tree needs additional touchscreen configuration.
---
# ⚠️ Important
The touchscreen works normally in the stock Android system.
Therefore:
> ✅ The touchscreen hardware appears to be functional.
Thе problem occurs only inside:
> ❌ TWRP Recovery
This makes the recovery environment, kernel, device tree, firmware loading, or driver initialization the most likely cause.
---
# 📌 Project Status
> 🟡 **TWRP boots successfully.**
> ❌ **Touchscreen is currently not working.**
> 🛠️ **FocalTech touchscreen initialization still needs to be fixed.**
> 🚧 **This project is still under development.**
---
# 🙏 Request for Help
If anyone has experience porting **TWRP to MediaTek devices** or working with **FocalTech touchscreen controllers**, I would greatly appreciate any help.
If you know what needs to be changed, added, or ported from the stock recovery/vendor environment, please let me know.
In particular, I am looking for help identifying the exact reason why the FocalTech touchscreen driver is not initializing in TWRP.
If additional logs or files are required, I can provide:
```text
dmesg
logcat
DTB
DTBO
vendor_boot.img
boot.img
stock recovery
kernel information
device tree files
```
Any suggestions, patches, configuration changes, or debugging instructions are very welcome.
---
# ❤️ Credits
Thanks to everyone working on:
- [TWRP](https://twrp.me/)
- KSN522
- Android custom recoveries
- MediaTek development
- Linux kernel development
- Android device trees
---
# 📄 License
This project is provided for development and research purposes.
Please respect the licenses of the original TWRP, Android, kernel, device tree, and vendor components used in this project.
---
# 🆘 If You Can Help
**Please open an Issue or leave a comment if you have an idea how to fix the FocalTech touchscreen.**
I would especially appreciate a working solution, patch, device-tree change, kernel configuration, or instructions for properly initializing the touchscreen in TWRP.
**Thank you for your help! ❤️**
