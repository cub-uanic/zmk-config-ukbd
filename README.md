# Kineziz Universal Keyboard Configuration

This repository contains the ZMK firmware configuration for multiple **Kineziz** keyboard variants using a **universal keymap** architecture.

## Supported Keyboards
| Variant | Shield | Board | Connection |
|---------|--------|-------|------------|
| Kineziz Advantage | `kineziz_adv` | `nice_nano_v2` | Wireless (BLE) |
| Kineziz Black | `kineziz_black` | `blackpill_f411ce` | Wired (USB) |

## Features
- **Universal Keymap**: Single `config/keyboard.keymap` shared across all variants.
- **Custom Layout**: Optimized Workman for Programmers on Mac.
- **Layers**: Unconvenient keys, F-keys, Mouse, Numpad, Arrow, and Macros.
- **Locked to ZMK v0.3.0**.

## Build and Flash
- [BUILD_GITHUB.md](BUILD_GITHUB.md): Automated builds via GitHub Actions.
- [BUILD_LOCAL.md](BUILD_LOCAL.md): Building locally using the `west` toolchain.

## How to Enable ZMK Studio
ZMK Studio support is currently disabled to keep the firmware lean. To enable it:

1.  **Configuration**: In [config/kineziz_adv.conf](config/kineziz_adv.conf), uncomment the following line:
    ```kconfig
    CONFIG_ZMK_STUDIO=y
    ```
2.  **Metadata**: In [boards/shields/kineziz_adv/kineziz_adv.zmk.yml](boards/shields/kineziz_adv/kineziz_adv.zmk.yml), uncomment the `studio` feature:
    ```yaml
    features:
      - keys
      - studio
    ```

## Project Structure
- `config/keyboard.keymap`: Universal keymap shared by all keyboards.
- `config/<shield>.keymap`: Shield-specific keymap wrapper (includes universal keymap).
- `config/<shield>.conf`: Shield-specific configuration.
- `boards/shields/kineziz_adv/`: Wireless Kinesis Advantage (nice!nano v2).
- `boards/shields/kineziz_black/`: Wired Kinesis Advantage (Blackpill F411CE).
- `boards/shields/tbkmini_5col/`: Wireless TBK Mini (5-Column variant).
- `boards/shields/tbkmini_6col/`: Wireless TBK Mini (6-Column variant).
- `build.yaml`: Build matrix for GitHub Actions.
- `zephyr/module.yml`: Registration for the repository as a ZMK module.

## License
MIT
