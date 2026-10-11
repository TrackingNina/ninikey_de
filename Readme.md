# ZigMKay Keycaprio German QWERTZ

Minimal [ZigMKay](https://github.com/EuroZig/zigmkay_firmware) firmware for the
[Leonardo Keycaprio](https://github.com/StephanMoeller/Leonardo-KeycapRio/) (34 keys, unibody, RP2040) with a QWERTZ keymap for the
German OS layout on Windows/Linux.

## Prerequisites

- [Zig `0.17.0`](https://ziglang.org/download/)

## Build

```bash
zig build                     # Keycaprio 0.7 (default)
zig build -Dkeycaprio=0.6     # Keycaprio 0.6
```

The firmware ends up at `zig-out/firmware/zigmkay.uf2`.

## Flash

Put the board into bootloader mode, then:

```bash
zig build flash               # add -Dkeycaprio=0.6 for the older PCB
```

On Windows this copies the UF2 to the mounted bootloader volume (picotool needs
a WinUSB driver there), elsewhere it uses `picotool`, which is built from source.
Pick a method explicitly with `zig build flash_pt` or `zig build flash_mount`
(`-Dflash-mount=<path|label>` overrides the default `RPI-RP2` volume).

## Layout

| File                            | Contents                                         |
|---------------------------------|--------------------------------------------------|
| `src/keymap.zig`                | Layers, combos and custom functions              |
| `src/main.zig`                  | Firmware entry point, selects the board pinout   |
| `src/boards/keycaprio_0_6.zig`  | Pins and key mapping of the 0.6 PCB              |
| `src/boards/keycaprio_0_7.zig`  | Pins and key mapping of the 0.7 PCB              |

Key indices (used by `sides`, the keymap layers and combos):

```
 0  1  2  3  4      5  6  7  8  9
10 11 12 13 14     15 16 17 18 19
20 21 22 23 24     25 26 27 28 29
         30 31     32 33
```

Layers: `L_BASE`, `L_ARROWS` (hold right space), `L_NUM` (hold left space),
`L_EMPTY`, `L_BOTH` (hold both spaces), `L_WIN` (hold `.`).
