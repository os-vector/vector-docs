# Partitions

Vector's partition table is pretty similar to that of an Android phone, except he has a couple extra ones added by Anki.

TODO

## OEM

Mounts to the /factory folder. Contains calibration logs and cloud keys which are used for mTLS.

## EMR

The EMR partiton (Electronic Medical Record) contains the calibration info of the robot, its ESN, its model number, and its packout status.

## boot_a and boot_b

These are the boot partitions. These partitons contain a ramdisk which is loaded which will then load a system partition matching the slot ID you are in.

## system_a and system_b

The partition Vector's full Linux OS exists in, corresponding to the boot slot. Slot a = system_a. Slot b = system_b.

## userdata

Encrypted, mounted to /data. Used to store user information like faces, pictures, and settings.