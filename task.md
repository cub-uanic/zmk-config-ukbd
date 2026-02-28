# Task: Multi-Keyboard ZMK Firmware Expansion

## Phase 0: Research & Planning
- [ ] Study reference project in `/Users/cub/projects/keyboard/zmk/zmk-config-ukbd/`
- [ ] Finalize Unified Implementation Plan

## Phase 1: Universal Keymap & Advantage Refactor
- [ ] Establish `config/keyboard.keymap` as the core universal keymap.
- [ ] Refactor `kinesis_micro` to `kineziz_adv`:
    - **Shield Name**: `kineziz_adv`
    - **Layout Logic**: Fixed matrix (Advantage style)
    - **MCU**: `nice_nano_v2`
    - **Features**: Wireless
    - **Branding**: "ZMK Kinesis Advantage"

## Phase 2: Kineziz Blackantage
- [ ] Implement `kineziz_adv` variant for Blackpill:
    - **Shield Name**: `kineziz_adv`
    - **Layout Logic**: Fixed matrix
    - **MCU**: `smt32f411`
    - **Features**: Wired
    - **Branding**: "ZMK Kinesis Blackantage"

## Phase 3: TBK Mini
- [ ] Implement `tbkmini` support:
    - **Shield Name**: `tbkmini`
    - **Layout Logic**: 3x6 split
    - **MCU**: `nice_nano_v2`
    - **Features**: Wireless split
    - **Branding**: "ZMK TBK Mini"

## Phase 4: Cygnus 46
- [ ] Implement `cygnus_46` support:
    - **Shield Name**: `cygnus_46`
    - **Layout Logic**: 4x6 split
    - **MCU**: `rp2040_zero`
    - **Features**: Wired split
    - **Branding**: "ZMK Cygnus RPZ"

## Phase 5: Charybdis RPi
- [ ] Implement `charybdis` wired variant:
    - **Shield Name**: `charybdis`
    - **Layout Logic**: 4x6 split
    - **MCU**: `rp2040_promicro`
    - **Features**: Wired + Trackball
    - **Branding**: "ZMK Charybdis RPi"

## Phase 6: Charybdis Wireless
- [ ] Implement `charybdis` wireless variant:
    - **Shield Name**: `charybdis`
    - **Layout Logic**: 4x6 split
    - **MCU**: `nice_nano_v2`
    - **Features**: Wireless split
    - **Branding**: "ZMK Charybdis"
