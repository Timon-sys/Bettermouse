# Better Mouse

A USB mouse remote for the Flipper Zero that actually feels like a mouse.

The stock USB Remote drives the pointer straight off the GUI input events, so
holding a direction gives you one 5 px nudge, then 300 ms of nothing, then a
burst of up to ten separate 20 px jumps every 150 ms. Better Mouse replaces that
with a real motion loop.

## What it does differently

- **Fixed-rate motion loop** (50 Hz by default, configurable) instead of the
  150 ms key-repeat rate, so movement is smooth and starts the instant you press.
- **Real diagonals** — velocity is a vector, scaled so diagonal is not 1.41x
  faster than straight.
- **Continuous acceleration** that eases from a pre-ramp speed up to your max,
  rather than jumping between a few fixed step sizes.
- **Sub-pixel accumulator**, so slow speeds actually work. HID reports are
  `int8`, and keeping the fractional remainder is what makes precise creeping
  possible instead of rounding to zero.
- **Stops dead on release.** Key state is read straight from the input service
  rather than the GUI queue, so a release is never delayed behind a redraw.
- **Ice mode** — optional momentum, where the pointer coasts to a stop.

## Controls

| Input | Action |
| --- | --- |
| Arrows | move |
| OK | left click |
| OK hold | drag lock — press OK again to drop |
| Back tap | right click |
| Back hold + OK | toggle scroll mode |
| Back hold 0.8s | drop to menu (warns first) |

The app opens straight into the mouse screen. Back from the menu exits.

## Settings

Everything is a wide open numeric range, not a handful of presets: max speed,
pre-ramp speed, accel ramp, scroll speed, report rate, ice glide, plus toggles
for ice mode, invert Y, invert scroll and click vibro.

One real ceiling worth knowing: HID reports are `int8`, so 127 px per report.
At 50 Hz that caps you around 6350 px/s no matter what you set — raise **Report
rate** to lift it.

## Build

Needs [ufbt](https://github.com/flipperdevices/flipperzero-ufbt) with the
Momentum SDK:

```
pip install ufbt
ufbt update --index-url=https://up.momentum-fw.dev/firmware/directory.json
ufbt              # build -> dist/bettermouse.fap
ufbt launch       # build, upload and run
```

Note: while the app is running it holds the USB port as a HID device, so the
serial port disappears and `ufbt launch` cannot reach the Flipper. Back out to
the Flipper menu first.

## Credits

- App icon by [SebStrt](https://github.com/SebStrt) 🎨
- Keypad artwork and the HID transport approach come from the USB Remote app in
  [Momentum Firmware](https://github.com/Next-Flip/Momentum-Firmware).
- This is my first actual Vibe code, and yes i do feel bad for it 😭

## License

GPL-3.0, matching the Flipper/Momentum firmware the bundled assets come from.
