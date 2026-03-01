# Implementation Plan: Unified Multi-Keyboard Configuration

This plan establishes a "Universal Layout" architecture where a single keymap file serves multiple keyboards with different or the same physical matrices and different MCUs. We will use ZMK's `matrix-transform` and `physical-layout` to map a shared logical keymap onto varying hardware.

1. Always create a plan first
2. Ask for confirmation before implementation
3. Implement step-by-step
4. Use context7-mcp to get all the latest information about ZMK (https://context7.com/zmkfirmware/zmk) and Zephyr (https://context7.com/websites/zephyrproject)

## User Review Required

> [!IMPORTANT]
> **Unified Keymap Strategy**: I will implement a single `config/keyboard.keymap` file.
> - Larger boards (Advantage) will use the full set of bindings.
> - Smaller boards (TBK Mini, Cygnus) will use a subset of these bindings, as mapped by their specific `matrix-transform`.
> - This allows you to maintain one set of macros and behaviors for all devices.

## Proposed Changes

### Stage 1: Advantage Refactor & Universal Keymap
- **Shield Name**: `kineziz_adv` (Renamed from `kinesis_micro`)
- **MCU Support**: `nice_nano_v2` (Wireless)
- **Core Task**: Establish `config/keyboard.keymap` as the generic universal layout.
- **Technical Detail**:
    - Use `RC()` macros for mapping logical keys to physical matrix positions.
    - Implement `kineziz_adv.matrix_transform.dtsi` for the Advantage-style fixed matrix.
    - Ensure `kineziz_adv.physical-layout.dtsi` is correctly defined for ZMK's layout metadata.
    - Rename `boards/shields/kinesis_micro` to `boards/shields/kineziz_adv`.

### Stage 2: Kineziz Blackantage
- **Shield Name**: `kineziz_adv`
- **MCU Support**: `blackpill_f411ce` (Wired)
- **Branding**: "Kineziz Black"
- **Technical Detail**:
    - **Ask user for already-existing files (gpio mapping and others)**.
    - Add `boards/blackpill_f411ce` directory with custom overlay/config.
    - Ensure the matrix transform is reused from the shield.
    - Target wired-only configuration (no BLE modules).

### Stage 3: TBK Mini
- **Shield Name**: `tbkmini`
- **Layout Logic**: 3x6 split
- **MCU**: `nice_nano_v2`
- **Features**: Wireless split
- **Branding**: "ZMK TBK Mini"
- **Technical Detail**:
    - **Ask user for already-existing files (gpio mapping and others)**.

### Stage 4: Cygnus 46
- **Shield Name**: `cygnus_46`
- **Layout Logic**: 4x6 split
- **MCU**: `rp2040_zero`
- **Features**: Wired split
- **Branding**: "ZMK Cygnus RPZ"
- **Technical Detail**:
    - **Ask user for already-existing files (gpio mapping and others)**.

### Stage 5: Charybdis RPi
- **Shield Name**: `charybdis`
- **Layout Logic**: 4x6 split
- **MCU**: `rp2040_promicro`
- **Features**: Wired + Trackball
- **Branding**: "ZMK Charybdis RPi"
- **Technical Detail**:
    - **Ask user for already-existing files (gpio mapping and others)**.

### Stage 6: Charybdis Wireless
- **Shield Name**: `charybdis`
- **Layout Logic**: 4x6 split
- **MCU**: `nice_nano_v2`
- **Features**: Wireless split
- **Branding**: "ZMK Charybdis"
- **Technical Detail**:
    - **Ask user for already-existing files (gpio mapping and others)**.

## Verification Plan

### Automated Tests
- **Build Matrix**: Update [build.yaml](file:///Users/cub/projects/keyboard/zmk-config-ukbd/build.yaml) to include all distinct build targets.
- **Syntax Validation**: Ensure the single `keyboard.keymap` is valid for all matrix sizes.

### Manual Verification
- **Shield Discovery**: Verify `west build` finds the correct shield for each unique command.
- **Layout Accuracy**: Flash `kineziz_adv` (Advantage) and verify that the layout and macros work exactly as they did before the refactor.
