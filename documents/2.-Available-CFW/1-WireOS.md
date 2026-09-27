# WireOS

WireOS is an OS created by Wire / kercre123.

Wire's goal is to provide a stable, up-to-date, and easily-buildable base for others to clone and modify.

It is based off of the leaked 2.0.1.6076 source code.

## Changes made compared to normal DDL firmware

- More normal-looking eyes on Vector 2.0
- A fixed loosepixel animation
- "unintentional performances" and "intentional performances"
    - Anki-created PR which was never merged
    - It makes him do the binaryeyes and tangram animations on his own sometimes
- Fixes an EMR reading bug
    - In the original code, the LCD drawing code would read the EMR partition upon every single LCD draw (30 times per second). This seems to have caused I/O weirdness
    - It reads the EMR partition for the hardware model version. Vector 1.0 and 2.0 screens are different, and the code must adjust for that
    - I made it so it only reads on LCD init
- Uses the Picovoice Porcupine wakeword engine
    - You can customize the wakeword in the `wired` webserver
- Includes `wired`
    - "Wire Daemon"
    - A special webserver program (at :8080) which is where custom wake word training happens, allows you to set the CPU/RAM frequency profile, allows you to opt-out of auto-updates, and lets you set other settings.
- OS and toolchain upgrade
    - Original OS was built from an ancient Qualcomm BSP based on Yocto Jethro (2015)
    - WireOS is now built with the latest Yocto LTS release as of September 2026 (Wrynose)
    - Clang 20 is now being used for the `victor` software rather than 5.0.1
    - msm-3.18 -> msm-4.9 kernel
        - Vector now uses 4.9.277 / LF.UM.8.7, the latest kernel released by Qualcomm for this chip
    - softfp -> hardfp
        - Vector had a softfp OS forever due to soft blobs which had to run. After a bit of shimming, everything now works in a hardfp OS, and the OS is now compiled as hardfp.
        - Brings software compatibility up to ~Pi 2
- Gamma correction
    - His camera now has much less trouble with brightly lit objects
    - Was an Anki-era PR, not my work
- Rainbow eyes
    - If chosen, his eyes will always cycle through all the hues
    - (this can be chosen in :8888/demo.html)
- Okao/OMROM facial recongition+detection replaced with YuNet+MobileFaceNet
- GPU is now actually being utilized to accelerate the new face models
- More up-to-date libraries
    - TensorFlow v2.19.0
        - Gives us XNNPACK and an OpenCL delegate
    - OpenCV 4.12.0
        - Resulted in much better SDK camera streaming performance
- [Face overlays](https://github.com/os-vector/wire-os-victor/pull/17)

## Installation

### Unlocked Prod

Use this if you have a prod robot which you unlocked with unlock-prod.ota.

There are a few ways to install WireOS in this case.

1. WireOS is available at [froggitti's Dev Vector web setup](https://websetup.froggitti.net) under the Custom Firmware stack.

2. Or, in the BLE terminal in recovery, after connecting him to Wi-Fi:

```
ota-start http://ota.pvic.xyz/vic/latest/dev.ota
```

3. Or, while SSHed into another CFW:

```
update-os http://ota.pvic.xyz/vic/latest/dev.ota
```

### PVT prototype running some sort of dev OTA (like 1.6.0.3331d)

```
systemctl stop anki-robot.target
mount -o rw,remount,exec /data
curl -o /data/update-engine http://ota.pvic.xyz/update-engine
chmod +rwx /data/update-engine
/data/update-engine http://ota.pvic.xyz/vic/latest/dev.ota -v
```

### OSKR

Use this if you unlocked your robot via DDL's official unlock program.

```
systemctl stop anki-robot.target
mount -o rw,remount,exec /data
curl -o /data/update-engine http://ota.pvic.xyz/update-engine
chmod +rwx /data/update-engine
/data/update-engine http://ota.pvic.xyz/vic/latest/oskr.ota -v
```
