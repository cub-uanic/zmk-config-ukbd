# Building with GitHub Actions

This repository is configured to build your ZMK firmware automatically using GitHub Actions.

## Prerequisites
- A GitHub account.
- This repository pushed to your GitHub account.

## How to Build

1.  **Commit and Push**: Every time you push changes to your `.keymap` or `.conf` files in the `config/` directory, GitHub will automatically start a build.
2.  **Monitor Progress**: 
    - Go to your repository on GitHub.
    - Click on the **"Actions"** tab.
    - You will see a workflow named **"Build"**. Click on the latest run to see details.
3.  **Download Firmware**:
    - Once the build is successful (green checkmark), scroll down to the **"Artifacts"** section at the bottom of the run page.
    - Download the `firmware.zip` (or the artifact named after your board/shield).
    - Unzip to find the firmware file(s).

## Build Matrix

The following targets are built automatically (see `build.yaml`):

| Target | Board | Shield | Output |
|--------|-------|--------|--------|
| Kineziz Advantage | `nice_nano_v2` | `kineziz_adv` | `zmk.uf2` |
| Kineziz Black | `blackpill_f411ce` | `kineziz_black` | `zmk.uf2` + `zmk.bin` |
| Settings Reset | `nice_nano_v2` | `settings_reset` | `zmk.uf2` |

## Flashing

### nice!nano v2 (Kineziz Adv)
1.  Double-tap the reset button to enter bootloader mode.
2.  Copy `zmk.uf2` onto the `NICENANO` USB drive.

### Blackpill F411CE (Kineziz Black)
1.  Double-tap the RESET button to enter UF2 bootloader mode.
2.  Copy `zmk.uf2` onto the USB drive.

> [!NOTE]
> The BlackPill firmware requires the **WeAct UF2 bootloader** to be installed.
> See [BUILD_LOCAL.md](BUILD_LOCAL.md) for detailed flashing instructions including DFU and manual UF2 conversion methods.

## Troubleshooting
- If the build fails, click on the **"build"** job in the Actions run to see the logs. Error messages in the `West Build` step usually point to syntax errors in your `.keymap` or `.dtsi` files.
