# Vector's OS

Vector runs on an embedded Linux image built with Yocto Jethro.

## What is Yocto?

Yocto is a toolkit for creating your own embedded Linux "distribution".

Vector does not "run Yocto Linux"!

He runs embedded Linux which happens to be *built with* Yocto.

## (original) OS details

- This is true for all Anki/DDL-created firmware:
    - Yocto Jethro
    - maintained 2015-2017
    - glibc 2.22
    - softfp linking

## Why softfp + what that means

Qualcomm provides proprietary binary "blobs" for some hardware communication. These are required for Bluetooth and camera functionality. These were built to run in an Android environment, and 32-bit Android is built with `softfp` for historical reasons, so the blobs were also built with `softfp`.

This means that pre-compiled shared libraries made for SBCs like the Raspberry Pi won't work unless you jump through a few hoops.

Example: Picovoice Porcupine, the new wake-word engine for WireOS, is shipped as a static library for various platforms. To get this to work in Vector's OS, I had to statically compile a `pv_server` program and have `vic-anim` communicate with it via IPC.

## Kernel

Vector runs an older version of the msm-3.18 kernel (3.18.66).

## Efforts to upgrade this

WireOS is now using a the latest possible Yocto base - Yocto Walnascar. It uses glibc 2.41 (latest as of 2025).

This means that *all* new CFW uses this base.

## History

DVT1 and early DVT2 prototype Vectors ran Android 7.1. Anki didn't really use any of the Android bits, and just dug down to the bare Linux underneath. They only used it while they were figuring out how to get Yocto working.