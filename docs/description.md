A USB mouse remote for the Flipper Zero that actually feels like a mouse.

The stock USB Remote drives the pointer straight from GUI key events, so holding
a direction gives one small nudge, then a pause, then bursts of large jumps.
Better Mouse replaces that with a proper motion loop.

## What it does differently

* Fixed rate motion loop, 50 Hz by default and configurable, instead of the
  150 ms key repeat, so movement starts the instant you press and stays smooth.
* True diagonals. Velocity is a vector, scaled so diagonal movement is not
  1.41 times faster than moving straight.
* Continuous acceleration that eases from a pre-ramp speed up to your maximum,
  rather than jumping between a few fixed step sizes.
* Sub-pixel accumulation, so slow speeds actually work. HID reports are 8-bit
  integers, and keeping the fractional remainder is what makes precise creeping
  possible instead of rounding away to nothing.
* Stops dead on release. Key state is read straight from the input service, so a
  release is never delayed behind a screen redraw.
* Ice mode, an optional momentum mode where the pointer coasts to a stop.

## Controls

* Arrows: move
* OK: left click
* OK held: drag lock, press OK again to drop
* Back tap: right click
* Back held plus OK: toggle scroll mode
* Back held for 0.8 seconds: drop to the menu

The app opens straight into the mouse screen, ready to use.

## Settings

Every value is an open numeric range rather than a handful of presets: maximum
speed, pre-ramp speed, acceleration ramp, scroll speed, report rate and ice
glide, plus toggles for ice mode, invert Y, invert scroll and click vibration.

One ceiling worth knowing: a HID report carries at most 127 pixels, so at 50 Hz
the pointer tops out around 6350 pixels per second no matter what you set.
Raise the report rate to lift it.

## Credits

App icon by [SebStrt](https://github.com/SebStrt). Keypad artwork and the HID
transport approach come from the USB Remote app in the Flipper Zero firmware.
