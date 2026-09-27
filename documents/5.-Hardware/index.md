# Hardware

Vector has two main PCBs: a headboard and a bodyboard.

TODO: these should be their own pages, each with pictures

## Headboard

The headboard is host to the main SoC, storage, RAM, camera, screen, Wi-Fi, BLE, IMU, and PMIC. It is the brains.

-   SoC: Qualcomm APQ8009
    -   Essentially a Wi-Fi-only version of the MSM8909v2
    -   Quad-core Cortex-A7
        -   Max clock: 1.3GHz
        -   Vector is limited to 533 MHz to prevent overheating and to reduce power usage
            -   This can be increased with cpufreq
    -   Adreno 304
        -   Weak, but can theoretically handle some AI tasks better than the CPU
        -   Anki experimented with this, but never ended up actually using it
    -   One quirk: the ADSP is disabled, and the MDSP is repurposed as the ADSP.
-   eMCP: Kingston 04EMCP04-NL3DM627
    -   4GB eMMC storage, 4Gb DDR3 RAM
        -   (4Gb = 512MB)
    -   eMCP = storage and RAM on one chip
-   Screen
    -   Vector 1.0: 184x96, accepts RGB565 data over SPI
    -   Vector 2.0: 160x80, accepts *bswapped* RGB565 data over SPI
-   Camera
    -   Vector 1.0: GC1066, 1280x720, 90 degree FoV
    -   Vector 2.0: BF2253L, 1600x1200
-   WLAN/BLE: WCN3610
    -   2.4 GHz 802.11n only
-   PMIC: Qualcomm PM8916
-   IMU: BMI160

## Bodyboard

The bodyboard is where all the robot bits (motors, sensors) connect to.

-   MCU: STMicroelectonics STM32F030C8
    -   8K RAM, 64K ROM
    -   Takes data from the sensors, outputs it into frames which the head can understand
    -   Receives data from the head, outputs it to the analog components (motors, LEDs)
-   Cliff sensors: 4 Lite-On proximity sensors
-   Each motor has an encoder, it is unknown where these come from
-   The gearboxes and motors are custom
    -   The motors are a standard size, but Anki had a custom winding
    -   Replacements might work, but maybe not as well
-   Distance sensor: STMicroelectonics VL530LX
-   Battery: FullRiver 320MaH
    -   TODO: replacement battery links

## Vector 1.0 vs. Vector 2.0

Vector 1.0 and 2.0 are essentially the same in every regard, except for the screen, camera, and addition of a removable battery compartment in 2.0.

These differences were already laid out above. A couple extra notes:

- Vector 1.0's camera is arguably better than 2.0's. The sensor size is basically the same, thus 2.0's camera lets in less light, which causes the image to have bad HDR and contrast.
- Vector 1.0's screen is also better than 2.0's. Bigger, higher res.
- **All modern CFW is PERFECTLY compatible with both Vector 1.0 and 2.0.**
  - All modern CFW is based on WireOS, which itself is based on an official DDL release (2.0.1) which officially supports both robots