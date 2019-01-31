#  MSI GL72M 7RDX Hackintosh Laptop

This is a Clover install for MacOS High Sierra 10.13.6. Still a few things to address, but the major stuff work properly.

### MSI GL72M 7RDX Laptop Specs
- Core i7 7700HQ
- Intel HD 630
- GeForce® GTX 1050 with 2GB GDDR5
- Intel® HM175 chipset
- Realtek ALC898
- 17.3" HD display 1920x1080
- 16gb 2400mhz DDR4
- 1TB Seagate FireCuda ST1000LX015
- Broadcom DW1820A BCM94350ZAE 2.4G/5G Dual Band 867Mbps M.2 NGFF WiFi Card with Bluetooth 4.1

### Functioning Components 

- [x] Intel HD 630 1536mb working
- [x] Wifi  
- [x] USB C/3.0 
- [x] Ethernet port
- [x] Audio 
- [x] Microphone
- [x] Webcam 
- [x] iMessage/Facetime
- [x] Sleep/Wake functionality
- [x] Keyboard brightness 

### Non-Functioning Components

- [ ] nVidia GTX 1050 does work, but I've disabled it in my build
- [ ] Bluetooth isn't working on the new card
- [ ] Brightness controls
- [ ] SD card reader
- [ ] Display Port
- [ ] HDMI regression, worked before switching to WhateverGreen

## Upgrades

### Wifi Card
I purchased a Broadcom DW1820A BCM94350ZAE 2.4G/5G Dual Band 867Mbps M.2 NGFF WiFi Card with Bluetooth 4.1 and swapped it into the laptop. Totally voided the warranty in the process.

### Hard Drive
Swapped out the stock drive for a Seagate FireCuda ST1000LX015 - hybrid hard drive - 1 TB - SATA 6Gb/s

### USB C Hub
Hub works and allows me to plugin additional USB items and read SD cards, but ethernet and HDMI passthrough do not work currently.

### WD Blue 3D NAND 250GB PC SSD - SATA III 6 Gb/s M.2 2280 Solid State Drive
New drive is in the mail. Looking forward to getting this going as my boot drive. 

## Installation Notes

### Fixing Bluetooth on BCM94350ZAE
Installed latest BrcmFirmwareRepo.kext and BrcmNonPatchRAM2.kext from https://bitbucket.org/RehabMan/os-x-brcmpatchram/downloads/ using Kext Utility to Library/Extensions. Did not work.

### Audio using WhateverGreen
- Replaced the AudioPatcher method with an entry under Devices->Properties Devices: PciRoot(0x0)/Pci(0x1f,0x3) Properties Key:layout-id Properties Value: 62000000 Value Type: Data

### Webcam Functionality
- The webcam does work, though it needs to be activated using the keyboard shortcut of Function + F6. I found this is a little sketchy as it didn't work if I needed it in the browser unless I already had the webcam active in Photo Booth after using the shortcut. Though once I had it working, it seems to be working on-going without needing to be pre-started like that.

### Screen Brightness / Sleep Wake
- Screen brightness still isn't working, but I do now have a control. It appeared after I followed these steps in [this forum post](https://www.tonymacx86.com/threads/solved-black-screen-after-upgrade-to-high-sierra.237050/page-2#post-1633911).
- In following the same process I was able to get the sleep/wake working. I implemented the settings found in [RehabMan's config_HD615_620_630_640_650_spoof.plist](https://github.com/RehabMan/OS-X-Clover-Laptop-Config/blob/master/config_HD615_620_630_640_650_spoof.plist) to my config and got wake to work. The outstanding issue is when it wakes there is a flicker to the screen.
- Implemented WhateverGreen Device/Property patches and finally got rid of the flicker 

### Sleep Working
- I followed [this post](https://www.tonymacx86.com/threads/guide-msi-gf62vr-7rf-high-sierra-10-13-2.241725/) and was able to adapt the approach from a similar MSI laptop to get it working for my laptop
- There are still some weirdness, but the machine will truly go to sleep. I need to activate it by going to Apple->Sleep for it to work. This will turn off the backlight of the keyboard and result in the power button glowing in and out blue. Just going to my hot corner or letting the machine just go to sleep on it's own just seems to put the monitor to sleep.
- When the laptop wakes the light switches from blue to red, indicating that it's switched to the GTX 1050 to run. I'm honestly not sure how that works, since I've disabled the card, but when running that card, the brightness controls work. 

### Restart on Shutdown Fix
- Added FixShutdown fix in Clover Configurator
- Turned off "Wake for network access" in Energy Preferences

### WhateverGreen & IntelGraphicsDVMTFixup
- Was able to replace IntelGraphicsDVMTFixup using [this patch](https://github.com/acidanthera/WhateverGreen/blob/master/Manual/FAQ.Intel.md)

### Updated BIOS
- Lost keyboard and mouse usage until I updated the DSDT from the new BIOS

### Getting the GTX 1050 working
- I was able to get NVidia card functioning. I installed the NVidia Web Drivers and CUDA, but just found there it didn't get me much further ahead than with the HD 630. May revisit at some point.
- If you're interested in messing around with it, there's an EFI folder called EFI-gtx-1050-working

## Useful Resource Links
- Successful GL72M 7RDX Sierra build - https://www.tonymacx86.com/threads/msi-gl72m-7rdx-sierra-10-12-6-succes.236359/
- Sleep/wake for HD 630? - https://www.reddit.com/r/hackintosh/comments/9fsf18/should_i_be_able_to_achieve_sleepwake_intel_hd/
- USB port limit fix - https://hackintosher.com/forums/thread/list-of-hackintosh-usb-port-limit-patches-10-14-updated.467/
- Framebuffer stuff https://www.insanelymac.com/forum/topic/334899-intel-framebuffer-patching-using-whatevergreen/
- WhateverGreen Audio (unimplemented) - https://www.tonymacx86.com/threads/guide-intel-framebuffer-patching-using-whatevergreen.256490/post-1790068

### Keyboard Usage Notes
- The brightness controls seem to be similar to where they'd appear on a Mac keyboard, using the scroll lock and pause break button. Using the function + up/down doesn't seem to do anything
- Function is mapped to the Option key
- Windows key is mapped to Function
- Function + F12 puts the laptop to sleep
- Keyboard brightness is function + plus/minus keys on the num pad