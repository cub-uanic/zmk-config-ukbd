# Implementation Plan: Unified Multi-Keyboard Configuration

This plan establishes a "Universal Layout" architecture where a single keymap file serves multiple keyboards with different or the same physical matrices and different MCUs. We will use ZMK's `matrix-transform` and `physical-layout` to map a shared logical keymap onto varying hardware.

1. Always create a plan first
2. Ask for confirmation before implementation
3. Implement step-by-step

## User Review Required

> [!IMPORTANT]
> **Unified Keymap Strategy**: I will implement a single `config/keyboard.keymap` file.
> - Larger boards (Advantage) will use the full set of bindings.
> - Smaller boards (TBK Mini, Cygnus) will use a subset of these bindings, as mapped by their specific `matrix-transform`.
> - This allows you to maintain one set of macros and behaviors for all devices.

## Proposed Changes

### Stage 1: Advantage Refactor & Universal Keymap
- **Shield Name**: `kineziz_adv` (Renamed from `kinesis_micro`)
- **Layout Logic**: Fixed matrix (Advantage style)
- **MCU**: `nice_nano_v2`
- **Features**: Wireless
- **Branding**: "ZMK Kinesis Advantage"
- **Core Task**: Establish `config/keyboard.keymap` as the generic universal layout.

### Stage 2: Kineziz Blackantage
- **Shield Name**: `kineziz_adv`
- **Layout Logic**: Fixed matrix
- **MCU**: `smt32f411`
- **Features**: Wired
- **Branding**: "ZMK Kinesis Blackantage"

### Stage 3: TBK Mini
- **Shield Name**: `tbkmini`
- **Layout Logic**: 3x6 split
- **MCU**: `nice_nano_v2`
- **Features**: Wireless split
- **Branding**: "ZMK TBK Mini"

### Stage 4: Cygnus 46
- **Shield Name**: `cygnus_46`
- **Layout Logic**: 4x6 split
- **MCU**: `rp2040_zero`
- **Features**: Wired split
- **Branding**: "ZMK Cygnus RPZ"

### Stage 5: Charybdis RPi
- **Shield Name**: `charybdis`
- **Layout Logic**: 4x6 split
- **MCU**: `rp2040_promicro`
- **Features**: Wired + Trackball
- **Branding**: "ZMK Charybdis RPi"

### Stage 6: Charybdis Wireless
- **Shield Name**: `charybdis`
- **Layout Logic**: 4x6 split
- **MCU**: `nice_nano_v2`
- **Features**: Wireless split
- **Branding**: "ZMK Charybdis"

## Verification Plan

### Automated Tests
- **Build Matrix**: Update [build.yaml](file:///Users/cub/projects/keyboard/zmk-config-ukbd/build.yaml) to include all distinct build targets.
- **Syntax Validation**: Ensure the single `keyboard.keymap` is valid for all matrix sizes.

### Manual Verification
- **Shield Discovery**: Verify `west build` finds the correct shield for each unique command.
- **Layout Accuracy**: Flash `kineziz_adv` (Advantage) and verify that the layout and macros work exactly as they did before the refactor.
