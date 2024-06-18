# Ubuntu Touch adaptation for the Lenovo Smart Tab M10 (X605F/X605L)
The repository supports Lenovo Tab M10 with Qualcomm Snapdragon 450 SoC, which may go under slightly different names in different countries and also referred as Lenovo TB-X605, where next letter is F for Wi-Fi-only and L for LTE-capable model.

This is based on Halium 9.0, and uses the mechanism described in [this page](https://github.com/ubports/porting-notes/wiki/GitLab-CI-builds-for-devices-based-on-halium_arm64-(Halium-9)).

This project can be built manually (see the instructions below) or you can download the ready-made artifacts from gitlab: take the [latest archive](https://gitlab.com/ubports/porting/community-ports/android9/lenovo-tab-m10-fhd/lenovo-x605/-/jobs/artifacts/focal/download?job=devel-flashable-focal), unpack the `artifacts.zip` file (make sure that all files are created inside a directory called `out/`, then follow the instructions in the [Install](#install) section.


## Install (first time)
 1. Unlock the device bootloader following usual unlock procedure (enable Developer mode, turn on "OEM unlocking" option, then reboot to bootloader and execute `fastboot flashing unlock`
 2. Flash Android 9 stock firmware using qdl utility from qualcomm (you can find more detailed instruction here: https://forums.ubports.com/post/71223):
    - Download stock rom for example from here: https://mirrors.lolinet.com/firmware/lenovo/Tab_M10/ (I used TB-X605L_S210224_200910_ROW.zip)
    - extract it
    - shut down and disconnect any cable from the device
    - within extracted folder execute `# qdl prog_emmc_firehose_8953_ddr.mbn rawprogram_unsparse_upgrade.xml patch0.xml`
      - it is now waiting for device edl mode
    - press both volume buttons at the same time and connect the usb-cable (which is connected to pc already), keep buttons pressed until something happens in the terminal
    - flash process should start
 3. Check that stock Android still boots (may take a few minutes for the first start), then reboot to bootloader again and execute the following commands with files downloaded from "devel-flashable-focal" job artifacts:
```bash
fastboot flash boot out/boot.img
fastboot flash system out/ubuntu.img
fastboot format:ext4 user-data
fastboot reboot
```

## Install/Update (UT is already installed)
Just repeat the flashing steps:
```bash
fastboot flash boot out/boot.img
fastboot flash system out/ubuntu.img
fastboot reboot
```