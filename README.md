###  MSI GL72M 7RDX Hackintosh Laptop

This is a Clover install for MacOS High Sierra 10.13.6

### Working 

- Intel HD 630 1536mb working
- Swapped in a Broadcom DW1820A BCM94350ZAE 2.4G/5G Dual Band 867Mbps M.2 NGFF WiFi Card with Bluetooth 4.1  
- USB C/3.0 hub seems to work and allow me to plugin additional USB items, but ethernet and HDMI passthrough do not work
- HDMI
- Ethernet port
- Webcam kinda works using Maccam (http://webcam-osx.sourceforge.net/downloads.html) though only through Photo Booth at the point. 

### Not Working Components

- nVidia GTX 1050 is disabled, may see about getting it working, which I why I stuck with High Sierra with this build as the Mojave drivers are still unreleased
- Audio is giving me trouble. I've been able to get volume controls to show up and internal speakers to show up in the sound preferences, but no actual sound output. When I plug in headphones I can hear clicking at the very top volume levels, but that's it. If I put on a video I can noise being output, but it's not actually the audio.
- Bluetooth isn't working on the new card
- Brightness controls
- Sleep/wake
- Brightness/dimming for keyboard
- Webcam funtionality through Skype/browser

### Untested Components
- Display port
- SD card reader


### Fixing Bluetooth on BCM94350ZAE

Installed latest BrcmFirmwareRepo.kext and BrcmNonPatchRAM2.kext from https://bitbucket.org/RehabMan/os-x-brcmpatchram/downloads/ using Kext Utility