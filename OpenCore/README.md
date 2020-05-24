#  MSI GL72M 7RDX Hackintosh Laptop

This is an OpenCore install for MacOS Mojave 10.15.3. This build is now a triple boot, Mojave, Windows 10 and Ubuntu build.

| MSI GL72M 7RDX Laptop Specs | |
| Core i7 7700HQ | |
| Intel HD 630 | |
| GeForce® GTX 1050 with 2GB GDDR5 | |
| Intel® HM175 chipset | |
| Realtek ALC898 | |
| 17.3" HD display 1920x1080 | |
| 16gb 2400mhz DDR4 | |
| 250GB WD Blue 3D NAND PC SSD | |
| 1TB ADATA SU800 SSD | |
| Broadcom DW1820A BCM94350ZAE 2.4G/5G Dual Band 867Mbps M.2 NGFF WiFi Card with Bluetooth 4.1 | |

### :thumbsup: Functioning Components 

- :white_check_mark: Intel HD 630 1536mb working
- :white_check_mark: Wifi  
- :white_check_mark: USB C/3.0 
- :white_check_mark: Ethernet port
- :white_check_mark: Audio 
- :white_check_mark: Microphone
- :white_check_mark: iMessage/Facetime
- :white_check_mark: Sleep/Wake functionality
- :white_check_mark: Keyboard brightness 
- :white_check_mark: Screen brightness adjustment
- :white_check_mark: Webcam
- :white_check_mark: HDMI
- :white_check_mark: Mini Display Port
- :white_check_mark: Ethernet through USB C

### :no_entry: Non-Functioning Components

- [ ] nVidia GTX 1050
- [ ] SD card reader

## :muscle: Upgrades

### Wifi Card
I purchased a Broadcom DW1820A BCM94350ZAE 2.4G/5G Dual Band 867Mbps M.2 NGFF WiFi Card with Bluetooth 4.1 and swapped it into the laptop. 

### USB C Hub
Hub works and allows me to plugin additional USB items and read SD cards, but HDMI passthrough do not work. The ethernet connection does work, so I can just plugin the hub and be connected to a wired connection automatically.

### WD Blue 3D NAND 250GB PC SSD - SATA III 6 Gb/s M.2 2280 Solid State Drive
Main boot drive for this machine.

### 1TB ADATA SU800 SSD
Windows and Ubuntu run off this drive, as well as a clone of the main SSD.

## :older_man: BIOS Configuration
The section below adapted from @0ranko0P's [MSI-GL62M 7RD Hackintosh](https://github.com/0ranko0P/GL62M-7RD-Hackintosh/blob/Catalina_DW1820A/README.md). This was huge, as I never knew how to access all the advanced settings in my BIOS.

**Some options only available in advanced mode:**\
In BIOS, holding **ALT + RIGHT-CTRL + SHIFT** together then press **F2**

| Settings |  |
|--|--|
| `CFG Lock` | Disable |
| `CSM` | Disable |
| Fast Boot | Disable |
| `Intel Speed Shift`(aka. HWP) | Enable |
| Secure Boot | Disable |
| Enable Hiberation | Disable |
| DVMT Pre-Allocated | 64M |

<pre>
[Advanced] tab
├─ Power & Performance
│  └─ CPU-Power Management Control
│     ├─ <b>Intel(R) Speed Shift Technology</b>
│     └─ CPU Lock Configuration
│        └─ <b>CFG Lock</b>
├─ System Agent (SA) Configuration
│  └─ Graphics Configuration
│     └─ DVMT Pre-Allocated
├─ CSM Configuration
│  └─ <b>CSM Support</b>
│   
└─ ACPI Settings
   └─ <b>Enable Hibernation</b>
</pre>

## ACPI Patching Notes
This laptop already has an embedded controller named EC in the DSDT, so it doesn't need to be patched.

## :notebook_with_decorative_cover: Installation Notes

### USB Port Limit 
I used Hackintool to fix my USB ports, along with a few other issues. It generated a new USBPorts.kext for my system and installed it in kexts/other. This iteration removes the MSI EPF USB and USB2.0-CRW SD Card Reader, as they serve no purpose.  

### Fixing the framebuffer
This has been the bane of my existence when it comes to this laptop. I finally got it working with OpenCore after ages of messing around with Hackintool patches, Skylake spoofs(that previously worked in Clover) and other people's MSI laptop setups. After recently learning how to access the BIOS settings to change the DVMT Pre-Allocated to 64m, which then allowed me to remove the 32mb DVMT-prealloc patches. Then after much trial and error, instead of using the [2 Intel HD Graphics 630 listed under Kaby Lake in the laptop guide](https://dortania.github.io/oc-laptop-guide/prepare-install-macos/display-configuration.html), I tried the Unlisted GPU `05001c59` mentioned right below them and now the LVDS screen no longer has a flicker. 

## :man_facepalming: Outstanding Issues

### Frontend Cleanup
Need to add a prettier boot screen and remove the debug kexts. 

### Bluetooth
Bluetooth does show up in Preferences, and it will attempt to connect to devices, but it can never seem to sustain a connection. 

### HDMI Audio 
I briefly had HDMI audio, but don't quite know what exactly it was that made it work. Need to focus on that one.

## Useful Resource Links
- [Vanilla Laptop Guide](https://dortania.github.io/oc-laptop-guide/)
- [MSI GP62 Hackintosh by Chuxubank](https://github.com/chuxubank/MSI-GP62-Hackintosh)

### :low_brightness: Keyboard Usage Notes
- The brightness controls seem to be similar to where they'd appear on a Mac keyboard, using the scroll lock and pause break button. Using the function + up/down doesn't seem to do anything
- Function is mapped to the Option key
- Windows key is mapped to Function, this setting is changed in the BIOS
- Function + F12 puts the laptop to sleep
- Keyboard brightness is function + plus/minus keys on the num pad

### :computer: USB Ports 
- HS03 USB2 <-- Top left USB2 port
- HS04 USB2 <-- Bottom left USB2 port
- HS05 TypeC+Sw <-- Orientation 1
- HS06 TypeC+Sw <-- Orientation 2
- HS07 Internal <-- MSI EPF USB
- HS08 USB2 <-- Right USB
- HS10 Internal <-- BCM2045A0 Bluetooth USB Port
- HS11 Internal <-- BisonCam, NB Pro
- HS12 Internal <-- USB2.0-CRW SD Card Reader
- SS02 USB3 <-- Bottom left USB3 port*******--
- SS03 USB3 <-- Top left USB3 port
- SS05 TypeC+Sw <-- Orientation 1
- SS06 TypeC+Sw <-- Orientation 2
