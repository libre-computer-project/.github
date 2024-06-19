# Libre Computer Design Stack

## Low Level Booting

* Each platform boots from an onboard ROM which is built into the SoC.
* On power-on, the ROM code will scan SPI or MMC devices for secondary bootloader based on a hardware defined configuration.
* Secondary bootloader software is platform-specific and does not work across platforms.
* Hardware defined configuration may be controlled via switches on specific platforms.
* Once the secondary bootloader loads, it provides UEFI abstraction for operating system images, isos, and network capability.
* We call the secondary bootloader "firmware".

## High Level Booting

* Firmware initializes board subsystems.
* Firmware loads [boot customization environment configuration](https://hub.libre.computer/t/how-to-customize-boot-logo-and-silence-the-logs-for-commercial-productization/2706) `boot.ini`.
* Firmware scans for bootable media [based on environment configuration](https://hub.libre.computer/t/how-to-change-boot-order-on-libre-computer-boards/4057).
* Firmware loads scripts, override device-trees, and/or UEFI applications into memory and runs them.
* Firmware provides device-tree or override device-tree to UEFI application.
* UEFI application is typically GRUB, systemd-boot, or Linux.

## Boards

* Libre Computer boards designed after 2018 have embedded the "firmware" on SPI NOR.
* They will boot to the UEFI graphical firmware interface layer on power on.
* There is a switch on these boards to disable the onboard firmware should an user decide to run custom firmware.
* Legacy boards designed prior to 2018 do not have SPI NOR so they do not boot to graphical interface.
* The "firmware" must be flashed correctly to an MMC device (SD or eMMC) so that the bot ROM can load it.
* If not flashed correctly, the board will not do anything on bootup or may appear to not power on in the case of ROC-RK3399-PC Renegade Elite.

### Legacy Boards prior to 2018 without Firmware

* ALL-H3-CC Tritium H3/H5
* AML-S905X-CC Le Potato
* ROC-RK3328-CC Renegade

### UEFI Boards with SPI NOR Firmware

* ALL-H5-CC Tritium Heavy
* AML-S805X-AC La Frite
* AML-S805X-AC-V2 Sweet Frite
* AML-S905X-CC-V2 Sweet Potato
* AML-S905D-PC Tartiflette
* AML-S905D3-CC Solitude
* AML-A311D-CC Alta
* ROC-RK3399-PC Renegade Elite
