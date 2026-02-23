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
    - Unzip the file to find `zmk.uf2`.

## Flashing

1.  **Connect Keyboard**: Plug in your keyboard to your computer via USB.
2.  **Bootloader Mode**: Double-tap the reset button on your nice!nano (or your specific MCU) to enter bootloader mode. The keyboard will appear as a USB mass storage device (e.g., `NICENANO`).
3.  **Copy File**: Drag and drop (or copy) the `zmk.uf2` file onto the USB drive.
4.  **Wait**: The drive will automatically unmount once the flashing is complete. Your keyboard is now running the new firmware!

## Troubleshooting
- If the build fails, click on the **"build"** job in the Actions run to see the logs. Error messages in the `West Build` step usually point to syntax errors in your `.keymap` or `.dtsi` files.
