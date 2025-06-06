# Tips For All

Tips and tricks for all - beginners, advanced users, and developers.

## Dual booting

Vector technically has three boot slots (boot slot = boot+system partition) - system_a, system_b, and recoveryfs.

We can swap between system_a and system_b.

The bot is in recovery when he is on the anki.com/dev screen. This should not be touched.

Let's say I want to run Viccyware in system_b, and WireOS in system_a. To do this:

1. Install WireOS like normal.
2. Once booted to WireOS, install Viccyware.

That's it!

Use the `sysswitch` command to swap between them.

If you are using an OS which doesn't have `sysswitch`, do the following to switch:

1. Run `cat /proc/cmdline`
2. If the output contains `androidboot.slot_suffix=_b` near the end, run `bootctl b set_active a`. If it is `androidboot.slot_suffix=_a`, run `bootctl a set_active b`.
3. Run `reboot`.

If the bootctl command gives you an errorish output, try `bootctl-anki` instead.

## CCIS

CCIS provides helpful information about Vector's network status, sensors, robot-specific-information like ESN, and OS information.

Do this to get to it:

1. Place Vector on the charger (important)
2. Double click the button
3. Lift the lift up then down (you are now in CCIS)
4. Push the head down then up
5. Click the button to go through the menus