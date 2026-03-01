# Task: Multi-Keyboard ZMK Firmware Expansion

1. Always create a plan first
2. Ask for confirmation before implementation
3. Implement step-by-step
4. Use context7-mcp to get all the latest information about ZMK (https://context7.com/zmkfirmware/zmk) and Zephyr (https://context7.com/websites/zephyrproject)


## Phase 0: Research & Planning
- [x] Study reference project in `/Users/cub/projects/keyboard/zmk/zmk-config-ukbd/`
- [x] Finalize Unified Implementation Plan

## Phase 1: Universal Keymap & Advantage Refactor
- [x] Establish `config/keyboard.keymap` as the core universal keymap.
- [x] Refactor `kinesis_micro` to `kineziz_adv`:
    - **Shield Name**: `kineziz_adv`
    - **Layout Logic**: Fixed matrix (Advantage style)
    - **MCU**: `nice_nano_v2`
    - **Features**: Wireless
    - **Branding**: "Kineziz Adv" (Shortened to fit BLE limit)
    - [x] Update `BUILD_LOCAL.md` for new naming
    - [x] Fix BLE device name length (max 16)
    - [x] Update `README.md` and configuration files

## Phase 2: Kineziz Blackantage
- [/] Implement `kineziz_adv` variant for Blackpill:
    - **Shield Name**: `kineziz_adv`
    - **Layout Logic**: Fixed matrix
    - **MCU**: `blackpill_f411ce`
    - **Features**: Wired
    - **Branding**: "Kineziz Black"
    - [ ] Ask user for existing GPIO mapping and files

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
