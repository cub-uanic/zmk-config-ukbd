# Kineziz Advantage ZMK Configuration

This repository contains the ZMK firmware configuration for the **Kineziz Advantage** keyboard using a **nice!nano v2** controller.

## Features
- **Custom Layout**: Optimized Workman for Programmers on Mac.
- **Layers**: Support for Unconvenient keys, F-keys, Mouse, Numpad, Arrow, and Macros.
- **Microcontroller**: nice!nano v2 (locked to ZMK v0.3.0).

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
- `config/`: Your keymap, feature settings, and workspace metadata.
- `boards/shields/kineziz_adv/`: Physical shield definition.
- `zephyr/module.yml`: Registration for the repository as a ZMK module.
- `build.yaml`: Build matrix for GitHub Actions.
- `config/west.yml`: Metadata for the `west` workspace.

## License
MIT
