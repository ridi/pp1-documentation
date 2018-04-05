Ridi output directory and A/S tool

This directory contains scripts Ridi uses for handling customer service.

You can either:
  - Copy contents of `rom` directory somewhere else and use independantly
  - Or use AS-IS, inside repository

## What each script does
### setup.h
  This script will:
  1. Check if required dependancies are installed (if not running on firmware build machine)
  2. Copy `adb`, `fastboot` binaries to /bin for easy global access (requires password for `sudo`)
  3. Download latest Ridi firmware images (user / userdebug) using `update_image.sh`
  4. Download waveform files using `update_waveform.sh`

### update_image.sh
  This script will download latest Ridi firmware images from AWS S3 and place them in:
  - `image` (user build with adb disabled)
  - `image_adb` (userdebug build with adb enabled, rootable using `adb root` command)

### update_waveform.sh
  This script will download all waveform images from AWS S3 and place them in `waveform_img`.

### fastboot_pcc.sh
  This script is Ridi customized version of `fastboot.sh` in root directory of `pp1` repository.
  This script provides simple text-based interface to install firmware and/or change serial number or waveform.

### write_sn.sh
  Script for replacing serial number only - requires ADB enabled device (eng or userdebug)

  Usage:
  ```
  ./write_sn.sh {new serial_number}
  ```

### write_vcom.sh
  Script for changing vcom value after changing EPD panel - requires ADB enabled device (eng or userdebug)

  Usage:
  ```
  ./write_vcom.sh {value}
  ```
  where `value` is VCOM value on the cable multipiled by -1000,
  ex) -1.37 => 1370


## Initial setup and usage
  - Use `setup.sh` when setting up tools for the first time,
  - Use `update_image.sh` for updating image files (if there's version update)
  - Use `update_waveform.sh` if waveform update is needed (contact Ridi if required waveform is not included)


## How to..

### Enable ADB on user build device
  1. `./setup.sh` (if not done before)
  2. `./fastboot_pcc.sh`
  3. Choose `4. Flash system image (ADB enabled)` (or 2 if there irreparable damage to data and everything needs to be wiped)
  4. Connect device in fastboot mode ([How-to](https://github.com/rbx-rdm/documentation#putting-device-in-fastboot-mode))
  5. Choose `3. Reboot`

### Replace EPD panel
  1. Replace EPD panel and check waveform and VCOM value (see Netronix manual [link](https://github.com/rbx-rdm/pp1/blob/master/ntx_addon/ntx_docs/EPD_maintenance_manual.docx))
  2. Continue if either waveform or VCOM value needs to be changed.
  3. `./setup.sh` (if not done before)
  4. Run `./fastboot_pcc.sh` and connect device in fastboot mode.
  5. Choose `4. Flash system image (ADB enabled)` (or 2 if there irreparable damage to data and everything needs to be wiped)
  6. (If waveform needs to be changed) Choose `2. Flash waveform` and choose correct waveform.
  7. Choose `3. Reboot`
  8. (If VCOM value needs to be changed) After reboot, use `./write_vcom.sh` script to change VCOM value.
  9. Run `./fastboot_pcc.sh` and connect device in fastboot mode.
  10. Choose `3. Flash system image (no ADB)`
  11. Choose `3. Reboot`
