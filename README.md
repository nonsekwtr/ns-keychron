# ns-keychron
This repository contains a collection of setup, customization and diagnostics guides I've encountered for Keychron keyboards, particularly the K4 Pro ANSI White model. I've also included steps for updating general and Bluetooth firmware update processes, as well as links to key tools and files.

_DISCLAIMER: I am not responsible for any loss of functionality or 'bricked' devices as a result of the advice below! Apply caution and be sure to use model-specific guides, tools, and files. To date, all tests and guides are based on my experience with the Keychron K4 Pro._

# General Setup and Diagnostics
_Get started with, and identify any issues that may have shipped with your Keychron keyboard._
- First connect your keyboard to your PC via USB cable (Keychron supplied cable is preferable). Ensure the toggle switch on the keyboard should is set to `Cable`.
- Open [Keychron Launcher](https://launcher.keychron.com/). Note: This requires a chromium-based broswer (Chrome, Opera, Brave, Edge, ...)
- Click `Connect` and select your keyboard model This will confirm your exact model, for example my K4 Pro is specifcally the K4 Pro White(CKBT).
- Confirm firmware is up to date under `Firmware` and `Wireless Firmware`. In my case only the model name is displayed.
- Test keys under `Key Test`, this may identify any issues that may be resolved by firmware updates (see below for detailed guides).

## Test Bluetooth/Wireless Connectivity
_Note: Keychron Launcher and other tools require a wired connection. Some models may have a different toggle switch label or location._
- Disconnect the USB cable and select the `BT` toggle switch position.
- Pair the keyboard to your device(s) via Bluetooth. I recommend testing this fucntionality for at least an hour or two, and switching between devices to see if any issues persist. Note: The toggle switch for wireless dongle connections may be labelled differently.

## Custom Keymaps (optional)

### Method 1: Keychron Launcher
_Note: you need to be connected to Keychron Launcher (see above) for this method._

- Under `Keymap`, take note of Layers. Typically, Layer 0 and Layer 1 are for iOS/macOS and Layer 2 and Layer 3 are for Windows/Android, which are selected with a toggle switch on the Keyboard. Layer 0 and Layer 2 show the base keymap. Layer 1 and Layer 3 show functions when `Fn + key` is pressed.
- Before changing default setup, I reccomend clicking `Export` and saving the current setupp as a backup `.json` file. 
- Experiment, make changes to the keymap and export your custom setup, giving it a different name. You can click `Import` to load the default `.json` file you saved earlier if you need to! Alternatively you can click `Reset` to revert to original settings

### Method 2: [VIA](https://www.usevia.app/) (third-party option)
_VIA is a keyboard diagnostic and configuration tool that works with multiple brands. It also provides general diagnostics. This also requires a chromium-based browser (Chome, Opera, Brave, Edge, ...)_
- You must be connected via USB cable to your PC.
- Find and download the `.json` keyboard definition file for your keyboard from [Keychron](https://www.keychron.com/pages/firmware). Note you will also need to know the layout of your model in addition to the LED config (White vs RGB), for example ANSI for US English, ISO for International.
- Extract the `.json` file (take note, there's both a standard, and MACOSX version).
- In VIA, Under the `Design` tab select `Load Draft Definition` and upload the `.json` file.
- Under the `Configure` tab select `Authorize Device` and select the keyboard model. Your model should appear at the top-right.
- Similar to the Keychron Launcher method, take note of the layers (top left) and save the default config as a `.json` file before making any custom changes as there is no reset option in VIA. Note: use the `SAVE + LOAD` button (bottom left) to do so.

# Firmware Updates
_Keychron states "Note: If everything works fine with your keyboard. Please don’t update the firmware. There is a chance it can damage your keyboard" and, I'm inclined to agree. As such, I am not responsible for any loss of functionality or 'bricked' devices!_

If you have issues with keyboard functionality, first peform a factory reset by pressing and hold `fn + J + Z` for 4 seconds and test if the issues persist. In my case, certain keys on the K4 Pro required multiple presses before registering, and a firmware update was required even after a factory reset.

## Keyboard Firmware Updates
_Keyboard must be connected by USB cable._

### Useful info:
- Refer to the [Keychron Firmware](https://www.keychron.com/pages/firmware) page to select your specific series/model.
- If you have a K series (non-Pro, non-Max) model, it is important to check that you get the correct firmware version, for example the K4 was produced in both [V1 and V2 versions](https://www.keychron.com/pages/keychron-firmware-for-k4), and each require different firmware. Older K series (non-Pro, non-Max) models use the `GateKeeper_Helper` firmware updater.
- In general Keychron recommends the Keychron Launcher method for all K, Q, V, and C (Pro and Max) series models for firmware updates, with specific `.bin` files for each model under the respective series pages.

### Method 1: Keychron Launcher
Refer to the [Keychron Offical Guide](https://www.keychron.com/blogs/news/how-to-restore-factory-settings-and-update-firmware-on-launcher). Follow these steps exactly, as failure to do so may result in a bricked keyboard. In brief, the steps are:

- Reset the keyboard: Press and hold `fn + J + Z` for 4 seconds. The keyboard backlight will flash for 3 seconds.
- Open [Keychron Launcher](https://launcher.keychron.com/) - establish a connection by clicking `Connect` and selecting your model.
- Under `Firmware`, you should see your keyboard model details and whether there is an upgrade to a newer version. _In my case only the model name is displayed, so I use QMK toolbox (see below)._
- If you can update the firmware, read the detailed steps carefully before following them exactly. Refer to the offical Keychron guide.

### Method 2: [QMK Toolbox](https://github.com/qmk/qmk_toolbox) (third-party option)
_QMK Toolbox is a firmware flashing tool available in Windows and macOS versions, and command line options for Linux users. Check out their [website](https://qmk.fm/) and [GitHub](https://github.com/qmk) for other tools and documentation._

Refer to [Flashing Your Keyboard with QMK Toolbox ](https://docs.qmk.fm/newbs_flashing#flashing-your-keyboard-with-qmk-toolbox) for detailed steps. In brief, the steps for Windows/macOS are:

- Download the latest `.bin` firmware file for your Keychron model [link](https://www.keychron.com/pages/firmware).
- Download, install, and run [QMK Toolbox](https://qmk.fm/toolbox)
- Put the keyboard in bootloader mode by pressing and holding `ESC`, unplugging the cable, and the plugging the USB cable back in. You should see `*** DFU device connected` appear in the QMK Toolbox console. If you do not, the keyboard is not in bootloder mode.
  - Alternatively, use the provided key puller to remove your spacebar key and locate the physical reset button on the PCB. Unplug and replug the USB cable while holding this button. 
- Load the firmware in QMK toolbox by clicking `Open` selecting the `.bin` file you downloaded, leave all other seetings as default.
- Click `Flash` (no longer greyed out if DFU device connected). You should see output in the concsole indicating a successful flash, followed by `*** DFU device disconnected`.
- You should have a successfully flashed keyboard.

QMK also provides firmware for non K and K Pro series Keychron models, such as C, Q, and V series models. If flashing with the official Keychron firmware doesn't yield desired results, consider selecting one of their [firmware files](https://browse.qmk.fm/). Use at your own risk, proceed with caution!

## Bluetooth Firmware Updates
_Keyboard must be connected by USB cable._

### Useful info:

- If you still have bluetooth connectivity issues after trying to resetting the keyboard by pressing and holding `fn + J + Z` for 4 seconds (the backlight with flash for 3 seconds), you may need to update bluetooth firmware.
- Refer to the official [Keychron Bluetooth Firmware page](https://www.keychron.com/pages/bluetooth-firmware) for guides and firmware specific to your model.
- In general all K Pro and Q Pro series models use the same `Bluetooth Firmware Tool - Keychron_Bt_Firmware_Upgrade_v0.14` flashing software and firmware version `v1.32`, as these have Bluetooth only.
- All V Max, Q Max, K Max, and newer versions of K (non-Pro, non-Max) series models use the `Keychron Firmware Updater - Keychron_Bt_Firmware_Upgrade_v1.02` flashing software and firmware version `v0.24`, as these have Bluetooth and 2.4G wireless connectivity.
- All older K series models have individual firmware pages. They all generally use the older OTA flashing software, but specific firmware `.hex` files per model.
- Installing the latest available firmware may solve connectivity issues, however some users' recommend installing firmware sequentially, as in the example below. It may be worth contancting Keychron support if you have continued Bluetooth issues after flashing. The example below shows that they have rolled more recent firmware updates in some cases, but haven't published these on their main site.
- Linux users: Keychron does not provide (as far as I know) cli tools or apps for Bluetooth firmware updates. Use a Windows or macOS system if possible.

### Example method: K Pro series with sequential updates
I followed this [guide on Reddit](https://www.reddit.com/r/Keychron/comments/1as61bs/finally_fixed_bluetooth_issues_for_k_pro_series/) where the user flashed firmware updates to the current `v1.32` version. Note: this may work for Q Pro series keyboards, with the same "use at your own risk, proceed with caution" caveat. I have largely improved connectivity, but still experience dropouts with the Qualcomm Atheros QCA61x4 adapater in myLenovo m715q tiny

- Go to [Keychron Bluetooth Firmware page](https://www.keychron.com/pages/bluetooth-firmware) and click [K Pro Series Bluetooth Firmware](https://www.keychron.com/pages/keychron-k-pro-series-bluetooth-firmware).
- Download, install, and run `Bluetooth Firmware Tool - Keychron_Bt_Firmware_Upgrade_v0.14` tool.
- Connect keyboard with USB cable
- Click `Get Version` and which will display the current Bluetooth firmware version. Even if your version is newer than `v1.32`, proceed below.
- Download the `v1.32` firmware file from this page and click `Browse` to open the file, and click Update.
- After the flash is complete, reset by pressing and holding `fn + J + Z` for 4 seconds (the backlight with flash for 3 seconds).
- Download [`v1.32-1`](https://keychronsupport.zendesk.com/attachments/token/kzBE17zKHIS1Ci51iOvYlB6hu/?name=keychron_ckbt51_01.32-1.kfw)
- Repeat the flash process and afterwards, reset by pressing and holding `fn + J + Z` for 4 seconds (the backlight with flash for 3 seconds).
- Download [`v1.32-2`](https://keychronsupport.zendesk.com/attachments/token/L8q5Y6u3IBvulxQirjf7KIDBZ/?name=keychron_ckbt51_01.32-2.kfw)
- Repeat the flash process and afterwards, reset by pressing and holding `fn + J + Z` for 4 seconds (the backlight with flash for 3 seconds).
- In your OS Bluetooth settings, un-pair ("forget this device") any instances of the paired keyboard, and pair it again.
- I've uploaded these files below in case the links to Keychron Support break.

# Quick summary
- Examples based on K Series, K4 Pro ANSI White model.
- Guides should be applicable to all K Pro and Q Pro models.
- Firmware update methods should apply to Q, V, and C (Pro and Max) series using model-specific `.bin` files. Note RGB color and layout!
- Bluetooth update method and firmware files should be aspplicable Q Pro series.

## Setup
- K4 Pro followed the same process as above
- VIA was used with success for custom keymap (see below). Keychron Launcher has not been tested.

## Key fixes
- Firmware updates fixed certain key presses failing to register.
- OMK Toolbox used instead of Keychron Launcher.
- Bluetooth connectivity issues improved under continued testing (see below).
- Bluetooth firmware update is sequential, `v1.32`, `v1.32-1`, `v1.32-2`, resetting keyboard between each flash, see example above. Files available below.

## Known Issues as of 2022-04-22
- Bluetooth timeouts on Qualcomm Atheros QCA61x4 in Lenovo m715q tiny. This is after repeated firmware updates to the Keyboard. Has to be used with a wired connection.


## Files (up-to-date as of 2026-04-22)
Keyboard definition file: 
[k4_pro_ansi_white_v1.01_20230807.json](k4_pro_ansi_white_v1.01_20230807.json)

Firmware: 
- [k4_pro_ansi_white_v1.01_20230807.bin](k4_pro_ansi_white_v1.01_20230807.bin)

Bluetooth Firmware Tool
- [Keychron_Bt_Firmware_Upgrade_v0.14.exe](Keychron_Bt_Firmware_Upgrade_v0.14.exe)

Bluetooth Firmware Files:
- [keychron_ckbt51_01.32.kfw](keychron_ckbt51_01.32.kfw)
- [keychron_ckbt51_01.32-1.kfw](keychron_ckbt51_01.32-1.kfw)
- [keychron_ckbt51_01.32-2.kfw](keychron_ckbt51_01.32-2.kfw)

Default keymap: 
- [keychron_k4_pro_ansi_white.layout.json](keychron_k4_pro_ansi_white.layout.json)

Custom keymap: 
- [ns_keychron_k4_pro_ansi_white.layout.json](ns_keychron_k4_pro_ansi_white.layout.json)
- Adds `INS (FN+DEL), Sleep (FN+HOME), Pause (FN+END), Print (FN+PGUP), Screen Shot (FN+PGDN)` to Layer 3 (Windows)

## Nice to haves
- Community discussion/inputs
- Additional Keychron models for experimentation
- Improved repo structure.
