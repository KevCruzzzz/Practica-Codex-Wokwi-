# Firmware Architecture

## Overview
The firmware is event-driven around keypad input polling. On each loop iteration:
1. Read a key from the 4x4 keypad.
2. If a valid key was pressed, execute one switch-case action.
3. Update one or more LEDs.
4. Delay for 10 ms.

Core behavior is intentionally preserved (no logic rewrites).

## Module Layout
- `src/main.cpp`
  - Global constants for LED count and keypad matrix dimensions.
  - Static pin maps for LEDs, keypad rows, and keypad columns.
  - `setup()` initializes all LED GPIOs to `OUTPUT` and sets LOW.
  - `loop()` reads keypresses and applies LED state transitions.

- `include/`
  - Reserved for future headers, abstractions, or board config files.

- `docs/wiring.md`
  - Electrical and GPIO mapping documentation.

## Key-to-Action Mapping
- Numeric keys `1..8`: turn on corresponding blue LED.
- `9`: turn on all blue LEDs (`LED1..LED8`).
- `0`: turn off all blue LEDs.
- `A..D`: turn on one corresponding red LED.
- `*`: turn on all red LEDs (`A..D`).
- `#`: turn off all red LEDs.

No keypress leaves outputs unchanged.

## Runtime Characteristics
- Polling period: nominal 10 ms (`delay(10)`).
- Debounce: primarily handled by keypad library and loop interval.
- State model: latching outputs (LEDs remain at last commanded state).

## Portability Notes
The current firmware uses Arduino APIs and `Keypad.h`. If building with native Pico SDK CMake, add compatibility layers or port logic to SDK GPIO APIs while preserving the exact behavior.
