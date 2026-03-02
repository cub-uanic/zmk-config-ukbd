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
# Kineziz Advantage (nice!nano v2, Wireless)
west build -p always -s zmk/app -b nice_nano_v2 -- \
  -DZMK_CONFIG="/Users/cub/projects/keyboard/zmk-config-ukbd/config" \
  -DZMK_EXTRA_MODULES="/Users/cub/projects/keyboard/zmk-config-ukbd" \
  -DSHIELD=kineziz_adv

# Kineziz Black (Blackpill F411CE, Wired)
west build -p always -s zmk/app -b blackpill_f411ce -- \
  -DZMK_CONFIG="/Users/cub/projects/keyboard/zmk-config-ukbd/config" \
  -DZMK_EXTRA_MODULES="/Users/cub/projects/keyboard/zmk-config-ukbd" \
  -DSHIELD=kineziz_black

# TBK Mini (nice!nano v2, Wireless Split, 6 Column)
west build -p always -s zmk/app -b nice_nano_v2 -- \
  -DZMK_CONFIG="/Users/cub/projects/keyboard/zmk-config-ukbd/config" \
  -DZMK_EXTRA_MODULES="/Users/cub/projects/keyboard/zmk-config-ukbd" \
  -DSHIELD=tbkmini_6col_left

west build -p always -s zmk/app -b nice_nano_v2 -- \
  -DZMK_CONFIG="/Users/cub/projects/keyboard/zmk-config-ukbd/config" \
  -DZMK_EXTRA_MODULES="/Users/cub/projects/keyboard/zmk-config-ukbd" \
  -DSHIELD=tbkmini_6col_right

# TBK Mini (nice!nano v2, Wireless Split, 5 Column)
west build -p always -s zmk/app -b nice_nano_v2 -- \
  -DZMK_CONFIG="/Users/cub/projects/keyboard/zmk-config-ukbd/config" \
  -DZMK_EXTRA_MODULES="/Users/cub/projects/keyboard/zmk-config-ukbd" \
  -DSHIELD=tbkmini_5col_left

west build -p always -s zmk/app -b nice_nano_v2 -- \
  -DZMK_CONFIG="/Users/cub/projects/keyboard/zmk-config-ukbd/config" \
  -DZMK_EXTRA_MODULES="/Users/cub/projects/keyboard/zmk-config-ukbd" \
  -DSHIELD=tbkmini_5col_right
```

> [!IMPORTANT]
> **Board Discovery Fixed**: We use `-DZMK_EXTRA_MODULES` instead of `ZEPHYR_EXTRA_MODULES`. This ensures that ZMK's internal board roots (including the `nice_nano_v2` board) are not overshadowed by the custom configuration module.

> [!WARNING]
> **Do NOT use `~` (tilde)**: CMake and Nano do not expand the tilde symbol correctly inside build arguments. Always use the full absolute path or `$HOME`.

*Replace `/Users/cub/projects/keyboard/zmk-config-ukbd` with the actual path to your repository on your machine.*

## Flashing

### nice!nano v2 (Kineziz Adv)
1.  Build output: `build/zephyr/zmk.uf2`
2.  Enter bootloader mode (double-tap reset).
3.  Copy `zmk.uf2` to the NICENANO drive.

### Blackpill F411CE (Kineziz Black)

The Blackpill F411CE uses the **WeAct UF2 bootloader**. The bootloader occupies the first 64KB (`0x10000`) of flash.

> [!IMPORTANT]
> **UF2 bootloader must be flashed first!** If your BlackPill doesn't have the WeAct UF2 bootloader installed, see [Installing UF2 Bootloader](#installing-uf2-bootloader-on-blackpill) below.

#### Method 1: UF2 (recommended)

The build is configured to automatically produce a UF2 file with the correct base address (`0x08010000`) and family ID (`0x57755a57`).

1.  Build output: `build/zephyr/zmk.uf2`
2.  Enter UF2 bootloader mode:
    - **Double-tap** the RESET button (or hold BOOT0 + tap RESET, depending on your bootloader version).
    - The board should appear as a USB mass storage device.
3.  Copy `zmk.uf2` to the mounted drive.

#### Method 2: Manual UF2 conversion (fallback)

If the automatic UF2 generation doesn't work with your bootloader, use the manual process:

```bash
# 1. Strip the ROM offset prefix from the BIN
dd if=build/zephyr/zmk.bin of=kineziz-black.bin bs=1 skip=$((0x10000))

# 2. Convert to UF2 with correct base address and family ID
python3 scripts/uf2conv.py \
  -c -b 0x08010000 -f 0x57755a57 \
  -o kineziz-black.uf2 kineziz-black.bin

# 3. Copy the UF2 to the mounted drive
```

> [!NOTE]
> The `uf2conv.py` script is bundled with Zephyr at `zephyr/scripts/build/uf2conv.py`, or you can get it from the [BlackPill UF2 Bootloader repository](https://github.com/WeActStudio/WeActStudio.STM32F4x1_UF2_Bootloader).

#### Method 3: DFU (no UF2 bootloader required)

If your BlackPill does **not** have the UF2 bootloader, you can flash directly via DFU:

```bash
# Enter DFU mode: hold BOOT0 + press RESET, then release BOOT0
dfu-util -d 0483:df11 -a 0 -s 0x08010000:leave -D build/zephyr/zmk.bin
```

### Installing UF2 Bootloader on BlackPill

If your BlackPill F411CE doesn't have the UF2 bootloader:

1.  Download the latest UF2 bootloader from [WeActStudio/WeActStudio.STM32F4x1_UF2_Bootloader](https://github.com/WeActStudio/WeActStudio.STM32F4x1_UF2_Bootloader/releases).
2.  Enter DFU mode: hold BOOT0 + press RESET, then release BOOT0.
3.  Flash the bootloader:
    ```bash
    dfu-util -d 0483:df11 -a 0 -s 0x08000000:leave -D bootloader-blackpill-f411ce.bin
    ```
4.  After the bootloader is installed, double-tap RESET to enter UF2 mode.

## STM32F411 Build Notes

> [!IMPORTANT]
> **ROM Offset**: The WeAct UF2 bootloader occupies the first 64KB of flash. `CONFIG_ROM_START_OFFSET=0x10000` is set in the shield config to ensure the firmware binary starts after the bootloader.

The following settings are automatically configured in `boards/shields/kineziz_black/kineziz.dtsi` (unified inline structure):
- `CONFIG_ROM_START_OFFSET=0x10000` — skip the bootloader region
- `CONFIG_BUILD_OUTPUT_UF2=y` — generate UF2 file
- `CONFIG_BUILD_OUTPUT_UF2_FAMILY_ID="0x57755a57"` — STM32F4 UF2 family ID

## Troubleshooting
- **Path Issues**: If you see "Unable to locate ZMK config", check that the path in `-DZMK_CONFIG` is absolute and the folder contains a `west.yml`.
- **Dirty Build**: If you encounter strange errors after changing configs, try a pristine build:
  ```bash
  west build -p always -s zmk/app ...
  ```
- **ZMK Version**: This config is locked to **ZMK v0.3.0**. Ensure your local environment is compatible with this version.
- **BlackPill UF2 not recognized**: Ensure the UF2 family ID matches your bootloader. Try `0x57755a57` (generic STM32F4) or `0x2dc309c5` (STM32F411xE-specific).
