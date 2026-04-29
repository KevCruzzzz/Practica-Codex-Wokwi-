# Wiring and GPIO Mapping (Raspberry Pi Pico W)

## Components (from `diagram.json`)
- 1x Raspberry Pi Pico / Pico W (`wokwi-pi-pico`)
- 1x 4x4 membrane keypad (`wokwi-membrane-keypad`)
- 12x LEDs (`wokwi-led`)
  - 8 blue LEDs labeled `1..8`
  - 4 red LEDs labeled `A..D`
- 12x LED current-limiting resistors (`220Ω`, `r1..r12`)
- 4x keypad pull-up resistors (`1kΩ`, `rp1..rp4`) tied to `3V3`

## GPIO Usage

### Keypad matrix
| Keypad Signal | Pico W GPIO |
|---|---|
| C1 | GP19 |
| C2 | GP18 |
| C3 | GP17 |
| C4 | GP16 |
| R1 | GP26 |
| R2 | GP22 |
| R3 | GP21 |
| R4 | GP20 |

### LED outputs
| LED Group | Logical Label | Pico W GPIO |
|---|---|---|
| Blue bank | LED 1 | GP11 |
| Blue bank | LED 2 | GP10 |
| Blue bank | LED 3 | GP9 |
| Blue bank | LED 4 | GP8 |
| Blue bank | LED 5 | GP7 |
| Blue bank | LED 6 | GP6 |
| Blue bank | LED 7 | GP5 |
| Blue bank | LED 8 | GP4 |
| Red bank | LED A | GP3 |
| Red bank | LED B | GP2 |
| Red bank | LED C | GP28 |
| Red bank | LED D | GP27 |

## Electrical Notes
- Every LED anode is driven by a GPIO through a `220Ω` resistor.
- Every LED cathode is tied to GND.
- Keypad row lines R1..R4 have discrete `1kΩ` pull-ups to `3V3` in the provided schematic.
- UART wiring exists in Wokwi (`GP0/GP1` to serial monitor) for console visibility.

## Assumptions
- The project code targets Arduino-style APIs (`setup()`, `loop()`, `Keypad.h`) running on RP2040-compatible tooling.
- The hardware diagram type is `wokwi-pi-pico`; for physical deployment, use Raspberry Pi Pico W pinout-equivalent GPIO numbers.
