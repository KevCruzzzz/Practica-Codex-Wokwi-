# Pico W Keypad-to-LED Controller

Documentation-first repository for a Raspberry Pi Pico W keypad/LED practice project created in Wokwi.

## Features
- 4x4 matrix keypad input on GPIO `GP16..GP22` + `GP26`
- 12 independent LED outputs on GPIO `GP2..GP11`, `GP27`, `GP28`
- Key-to-LED action map using straightforward switch-case logic
- Wokwi-friendly wiring and firmware layout

## Repository Structure

```text
.
├── CMakeLists.txt
├── diagram.json
├── src/
│   └── main.cpp
├── include/
└── docs/
    ├── architecture.md
    └── wiring.md
```

## Firmware Source
- Main firmware: `src/main.cpp`
- Core logic was preserved from the provided code (behavior unchanged).

## Quick Start (Wokwi)
1. Create/import project in Wokwi.
2. Use `diagram.json` wiring and `src/main.cpp` firmware.
3. Ensure RP2040-compatible toolchain/library supports `Keypad.h` and Arduino API.
4. Start simulation and press keypad buttons to verify LED behavior.

## Run on Real Raspberry Pi Pico W

### Option A: Arduino-Pico workflow (recommended for this exact source)
1. Install Arduino IDE + RP2040 board package.
2. Install `Keypad` library in Library Manager.
3. Open `src/main.cpp` as sketch source (or copy into `.ino` preserving content).
4. Select **Raspberry Pi Pico W** board and flash.
5. Wire hardware per `docs/wiring.md`.

### Option B: Native Pico SDK (advanced)
- `CMakeLists.txt` is provided as project scaffold.
- Because the source uses Arduino abstractions (`pinMode`, `digitalWrite`, `delay`, `Keypad.h`), native SDK builds require wrappers or source adaptation.
- Keep control logic identical if you port API calls.

## Flashing Notes
- Hold **BOOTSEL**, connect Pico W over USB, copy UF2 if using compiled UF2 workflow.
- Verify common GND between keypad/LED network and Pico W.

## Wi-Fi / Secrets
- This project does not currently use Wi-Fi APIs.
- If Wi-Fi is added later, store credentials in a separate ignored config file (e.g., `secrets.h` / `secrets.py`) and never commit plaintext credentials.

## Validation Checklist
- Press `1..8`: matching blue LED turns on.
- Press `9`: all blue LEDs on.
- Press `0`: all blue LEDs off.
- Press `A..D`: matching red LED turns on.
- Press `*`: all red LEDs on.
- Press `#`: all red LEDs off.
