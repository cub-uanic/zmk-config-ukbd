# Building ZMK Locally

This guide describes how to build your firmware using a local ZMK setup.

## Prerequisites
- [Git](https://git-scm.com/)
- [West](https://docs.zephyrproject.org/latest/develop/west/index.html) (Zephyr's meta-tool)
- [ZMK Toolchain](https://zmk.dev/docs/development/local-toolchain/setup) (Docker is recommended for the easiest setup).

## Setup (First Time Only)

1.  **Initialize Workflow**:
    ```bash
    # Create a workspace directory (outside this repo)
    mkdir zmk-workspace && cd zmk-workspace
    
    # Initialize the workspace using this config
    west init -m https://github.com/[YOUR_USERNAME]/zmk-config-ukbd --mr v0.3.0
    
    # Update modules
    west update
    
    # Export Zephyr CMake package
    west zephyr-export
    ```

## How to Build

From your workspace root (e.g., `zmk-workspace/`), run:

```bash
west build -s zmk/app -b nice_nano_v2 -- -DZMK_CONFIG="[PATH_TO_YOUR_CONFIG_REPO]/config" -DSHIELD=kinesis_micro
```

*Replace `[PATH_TO_YOUR_CONFIG_REPO]` with the absolute path to your local `zmk-config-ukbd` directory.*

## Flashing

1.  The build output will be located at `build/zephyr/zmk.uf2`.
2.  Connect your keyboard and enter bootloader mode (double-tap reset).
3.  Copy `zmk.uf2` to the NICENANO drive.

## Troubleshooting
- **Dirty Build**: If you encounter strange errors after changing configs, try a pristine build:
  ```bash
  west build -p -s zmk/app ...
  ```
- **ZMK Version**: This config is locked to **ZMK v0.3.0**. Ensure your local environment is compatible with this version.
