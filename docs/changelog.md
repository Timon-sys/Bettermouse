## v1.2

- Mouse screen title no longer overlaps the keypad graphic
- Speed values show as `2000/s` so four and five digit speeds are not clipped
- Ice glide adjustable in 10 ms steps
- App icon stored as a 1-bit PNG

## v1.1

- Pointer speed is now steady: the motion loop runs on absolute deadlines and
  integrates against measured elapsed time, removing a slow speed modulation
- Redrawing the speed bar no longer stalls the pointer during acceleration
- Ice mode: optional momentum, where the pointer coasts to a stop
- Pre-ramp speed, report rate and every other value are open numeric ranges

## v1.0

- First release
- Fixed rate motion loop instead of the 150 ms key repeat, so movement starts
  immediately and stays smooth
- True diagonals, sub-pixel accumulation, configurable acceleration
- Scroll mode, drag lock, adjustable speed and scroll settings
