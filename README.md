# Kinesis Micro ZMK Configuration

This repository contains the ZMK firmware configuration for the **Kinesis Micro** keyboard using a **nice!nano v2** controller.

## Features
- **Custom Layout**: Optimized Workman for Programmers on Mac.
- **Layers**: Support for Unconvenient keys, F-keys, Mouse, Numpad, Arrow, and Macros.
- **Microcontroller**: nice!nano v2 (locked to ZMK v0.3.0).

## Build and Flash
- [BUILD_GITHUB.md](BUILD_GITHUB.md): Automated builds via GitHub Actions.
- [BUILD_LOCAL.md](BUILD_LOCAL.md): Building locally using the `west` toolchain.

## How to Enable ZMK Studio
ZMK Studio support is currently disabled to keep the firmware lean. To enable it:

1.  **Configuration**: In [config/kinesis_micro.conf](config/kinesis_micro.conf), uncomment the following line:
    ```kconfig
    CONFIG_ZMK_STUDIO=y
    ```
2.  **Metadata**: In [boards/shields/kinesis_micro/kinesis_micro.zmk.yml](boards/shields/kinesis_micro/kinesis_micro.zmk.yml), uncomment the `studio` feature:
    ```yaml
    features:
      - keys
      - studio
    ```
3.  **Keymap (Optional but Recommended)**: In [config/kinesis_micro.keymap](config/kinesis_micro.keymap), find the `macro_layer` and uncomment the `&studio_unlock` behavior:
    ```c
    /* &studio_unlock */ ___x___  =>  &studio_unlock
    ```
    This allows secured access to Studio features from your keyboard.

## Project Structure
- `config/`: Keymap and user-level configuration.
- `boards/shields/kinesis_micro/`: Physical shield definition (matrix, pins).
- `build.yaml`: Build matrix for GitHub Actions.
- `west.yml`: Metadata for the `west` workspace.

## License
MIT
