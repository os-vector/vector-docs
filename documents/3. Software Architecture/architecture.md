# Vector's Software Architecture

Vector's software is broken up into quite a few components.

## The main OS

Vector runs Embedded Linux built with Yocto, using the systemd init system. His processes run as regular daemons.

## /anki

The /anki folder of the ext4 system partition is where the personality lives.

Built programs are in /anki/bin, libraries in /anki/lib, data (like animations and sounds) exists in /anki/data/assets/cozmo_resources, and environment files exist in /anki/etc.

The programs are the interesting parts. They communicate with each other via Unix sockets:

### vic-engine

- Handles A.I. (such as vision processing), SLAM, and personality. All of the programs inside of Vector eventually communicate with this.
- C++

### vic-anim

- Handles text-to-speech, animation playback, procedural eye rendering, sound playback, and wake-word recognition. For the most part, engine tells anim what to do, and anim performs it.
- C++

### vic-robot

- Handles communication with the body.
- C++

### vic-cloud

- Handles communication with the cloud: voice data (after the wake-word), jdocs (user information/settings), token (authentication).
- Go

### vic-gateway

- Handles SDK communications. It hosts Vector's port :443. It essentially takes in gRPC requests, parses them, then tells engine what to do depending on the contents of the requests. It can also grab data from engine.
- Go

### update-engine

- Handles OTA updates. A user can initiate this via BLE (or over SSH directly), or systemd can initiate it. A systemd timer daemon is set to initiate this a few times a day to check for updates from whatever URL is set in /anki/etc/update-engine.env.
- Python
    - Orignal OS: Python 2.7.3
    - Modern CFW: Python 3.13.2

