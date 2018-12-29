###  MSI GL72M 7RDX Hackintosh Laptop

This is a Clover install for MacOS High Sierra 10.13.6

### Working 

- Intel HD 630 1536mb working
- Swapped in a Broadcom DW1820A BCM94350ZAE 2.4G/5G Dual Band 867Mbps M.2 NGFF WiFi Card with Bluetooth 4.1  
- USB C/3.0 hub seems to work and allow me to plugin additional USB items, but ethernet and HDMI passthrough do not work
- HDMI
- Ethernet port
- Audio 
- Microphone

### Not Working Components

- nVidia GTX 1050 is disabled, may see about getting it working, which I why I stuck with High Sierra with this build as the Mojave drivers are still unreleased
- Bluetooth isn't working on the new card
- Brightness controls
- Sleep/wake
- Brightness/dimming for keyboard
- Webcam
- SD card reader

### Untested Components
- Display port


### Fixing Bluetooth on BCM94350ZAE

Installed latest BrcmFirmwareRepo.kext and BrcmNonPatchRAM2.kext from https://bitbucket.org/RehabMan/os-x-brcmpatchram/downloads/ using Kext Utility to Library/Extensions. Did not work.

### Fixed audio using AppleHDA Patcher 1.9
- Ran AppleHDA Patcher 1.9, dropped my config.plist and the latest AppleHDA.kext into the app
- Under laptop picked Realtek ALC 898
- Added CodecCommander.kext and aDummyHDA.kext to System/Library/Extensions and audio started working.


### Useful Resource Links
