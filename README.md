#  MSI GL72M 7RDX Hackintosh Laptop

This is a Clover install for MacOS High Sierra 10.13.2

### Functioning Components 

- Intel HD 630 1536mb working
- Wifi  
- USB C/3.0 hub seems to work and allow me to plugin additional USB items, but ethernet and HDMI passthrough do not work
- HDMI
- Ethernet port
- Audio 
- Microphone
- Webcam 

### Non-Functioning Components

- nVidia GTX 1050 is disabled, may see about getting it working, which I why I stuck with High Sierra with this build as the Mojave drivers are still unreleased
- Bluetooth isn't working on the new card
- Brightness controls
- Sleep/wake
- Brightness/dimming for keyboard
- SD card reader

### Untested Components
- Display port

## Upgrades

### Wifi Card
I purchased a Broadcom DW1820A BCM94350ZAE 2.4G/5G Dual Band 867Mbps M.2 NGFF WiFi Card with Bluetooth 4.1 and swapped it into the laptop. Totally voided the warranty in the process.

### Hard Drive
Swapped out the stock drive for a Seagate FireCuda ST1000LX015 - hybrid hard drive - 1 TB - SATA 6Gb/s

## Installation Notes

### Fixing Bluetooth on BCM94350ZAE

Installed latest BrcmFirmwareRepo.kext and BrcmNonPatchRAM2.kext from https://bitbucket.org/RehabMan/os-x-brcmpatchram/downloads/ using Kext Utility to Library/Extensions. Did not work.

### Fixed audio using AppleHDA Patcher 1.9
- Ran AppleHDA Patcher 1.9, dropped my config.plist and the latest AppleHDA.kext into the app
- Under laptop picked Realtek ALC 898
- Added CodecCommander.kext and aDummyHDA.kext to System/Library/Extensions and audio started working.
- Note injected audio ID is 98 for this MSI laptop. Seems a little unconventional, but it seems to be common on sibling model MSI laptops

### Webcam Functionality
- The webcam does work, though it needs to be activated using the keyboard shortcut of Function + F6. I found this is a little sketchy as it didn't work if I needed it in the browser unless I already had the webcam active in Photo Booth after using the shortcut. 


## Useful Resource Links

- Successful GL72M 7RDX Sierra build - https://www.tonymacx86.com/threads/msi-gl72m-7rdx-sierra-10-12-6-succes.236359/
- Sleep/wake for HD 630? - https://www.reddit.com/r/hackintosh/comments/9fsf18/should_i_be_able_to_achieve_sleepwake_intel_hd/