#  MSI GL72M 7RDX Hackintosh Laptop

This is a Clover install for MacOS Mojave 10.14.5. This build is now a triple boot, Mojave, Windows 10 and Ubuntu build.

### MSI GL72M 7RDX Laptop Specs
- Core i7 7700HQ
- Intel HD 630
- GeForce® GTX 1050 with 2GB GDDR5
- Intel® HM175 chipset
- Realtek ALC898
- 17.3" HD display 1920x1080
- 16gb 2400mhz DDR4
- 250GB WD Blue 3D NAND 250GB PC SSD
- 1TB Seagate FireCuda ST1000LX015
- Broadcom DW1820A BCM94350ZAE 2.4G/5G Dual Band 867Mbps M.2 NGFF WiFi Card with Bluetooth 4.1

### Functioning Components 

- [x] Intel HD 630 1536mb working
- [x] Wifi  
- [x] USB C/3.0 
- [x] Ethernet port
- [x] Audio 
- [x] Microphone
- [x] iMessage/Facetime
- [x] Sleep/Wake functionality
- [x] Keyboard brightness 
- [x] Screen brightness adjustment
- [x] Webcam
- [x] Bluetooth 
- [x] HDMI
- [x] Mini Display Port
- [x] Ethernet through USB C

### Non-Functioning Components

- [ ] nVidia GTX 1050 does work, but I've disabled it in my build
- [ ] SD card reader

## Upgrades

### Wifi Card
I purchased a Broadcom DW1820A BCM94350ZAE 2.4G/5G Dual Band 867Mbps M.2 NGFF WiFi Card with Bluetooth 4.1 and swapped it into the laptop. Totally voided the warranty in the process.

### Hard Drive
Swapped out the stock drive for a Seagate FireCuda ST1000LX015 - hybrid hard drive - 1 TB - SATA 6Gb/s

### USB C Hub
Hub works and allows me to plugin additional USB items and read SD cards, but HDMI passthrough do not work currently. The ethernet connection does work, so I can just plugin the hub and be connected to a wired connection automatically.

### WD Blue 3D NAND 250GB PC SSD - SATA III 6 Gb/s M.2 2280 Solid State Drive
Main boot drive for this machine.

### Seagate FireCuda ST1000LX015
Windows and Ubuntu run off this drive, as well as a clone of the main SSD.

## Installation Notes

### Fixing Bluetooth on BCM94350ZAE
Installed latest BrcmFirmwareRepo.kext and BrcmNonPatchRAM2.kext from https://bitbucket.org/RehabMan/os-x-brcmpatchram/downloads/ using Kext Utility to Library/Extensions. Had to make sure SIP was disabled first or this work. Found out why it wasn't working was because my USB ports were messed up. I used Hackintool 1.8.2 to figure out which ports were which and this got Bluetooth to show up in my system preferences. In fixing my HDMI by implementing RehabMan's [config_HD615_620_630_640_650.plist](https://github.com/RehabMan/OS-X-Clover-Laptop-Config/blob/master/config_HD615_620_630_640_650.plist) it seemed to fix my Bluetooth issues too.

**January 4, 2020 Update** It seems like a lingering issue with Bluetooth seems to have been fixed with the latest kext updates. I'd had issues with devices sustaining connections, but it seems to be working really well now.

### HDMI video out
It took me awhile to get this working, but using RehabMan's [config_HD615_620_630_640_650.plist](https://github.com/RehabMan/OS-X-Clover-Laptop-Config/blob/master/config_HD615_620_630_640_650.plist) I was able to get HDMI out working properly. 

### USB Port Limit 
I used Hackintool 1.8.2 to fix my USB ports, along with a few other issues. It generated a new USBPorts.kext for my system and installed it in kexts/other

### Audio using WhateverGreen
- Replaced the AudioPatcher method with an entry under Devices->Properties Devices: PciRoot(0x0)/Pci(0x1f,0x3) Properties Key:layout-id Properties Value: 62000000 Value Type: Data

### Webcam Functionality
- The webcam does work, though it needs to be activated using the keyboard shortcut of Function + F6. I found this is a little sketchy as it didn't work if I needed it in the browser unless I already had the webcam active in Photo Booth after using the shortcut. Though once I had it working, it seems to be working on-going without needing to be pre-started like that.

### Screen Brightness / Sleep Wake
- Screen brightness now works. I found [@goldenegg's MSI build](https://www.tonymacx86.com/threads/guide-msi-gf62vr-7rf-high-sierra-10-13-2.241725/) that was quite similar to mine and was able to get screen brightness working. This is huge as I'm not sure I've seen any other builds of similar gen MSI laptops running HD 630s that have this working.

**January 4, 2020 Update** For a spell only the brightness down was working, but recent kext updates seemed to have fixed that.

### Sleep Working
- I followed [this post](https://www.tonymacx86.com/threads/guide-msi-gf62vr-7rf-high-sierra-10-13-2.241725/) and was able to adapt the approach from a similar MSI laptop to get it working for my laptop
- Following the same instructions I was able to get true sleep and wake to work. The laptop will go to sleep on it's own and with the lid closed. The keyboard backlight turns off and everything.
- When the laptop wakes the light switches from blue to red, indicating that it's switched to the GTX 1050 to run. It doesn't seem to impact anything, so I'm not too bothered by it at this point.

### Restart on Shutdown Fix
- Added FixShutdown fix in Clover Configurator
- Turned off "Wake for network access" in Energy Preferences

### Getting the GTX 1050 working
- I was able to get NVidia card functioning. I installed the NVidia Web Drivers and CUDA, but just found there it didn't get me much further ahead than with the HD 630. May revisit at some point.
- If you're interested in messing around with it, there's an EFI folder called EFI-gtx-1050-working

### Display Port
Thanks to @effeci I was able to get the display port working. I needed to spoof my [Kaby Lake to Skylake](https://www.tonymacx86.com/threads/readme-common-problems-and-workarounds-on-10-14-mojave.255823/) and it started working properly.

### Added sound on startup
I discovered Clover will make a sound on bootup. I opted to find the old Mac bong sound that used to be there when you'd boot a Mac. Now your Hackintosh can sound more like a Mac than a real Mac does these days.

## Outstanding Issues

### SD Card Reader
I have a feeling this might actually work, just haven't tried yet.

### HDMI Audio 
Still haven't had the time to really test this one, just know it doesn't work currently.

## Useful Resource Links
- Successful GL72M 7RDX Sierra build - https://www.tonymacx86.com/threads/msi-gl72m-7rdx-sierra-10-12-6-succes.236359/
- Sleep/wake for HD 630? - https://www.reddit.com/r/hackintosh/comments/9fsf18/should_i_be_able_to_achieve_sleepwake_intel_hd/
- USB port limit fix - https://hackintosher.com/forums/thread/list-of-hackintosh-usb-port-limit-patches-10-14-updated.467/
- Framebuffer stuff https://www.insanelymac.com/forum/topic/334899-intel-framebuffer-patching-using-whatevergreen/
- WhateverGreen Audio - https://www.tonymacx86.com/threads/guide-intel-framebuffer-patching-using-whatevergreen.256490/post-1790068

### Keyboard Usage Notes
- The brightness controls seem to be similar to where they'd appear on a Mac keyboard, using the scroll lock and pause break button. Using the function + up/down doesn't seem to do anything
- Function is mapped to the Option key
- Windows key is mapped to Function, this setting is changed in the BIOS
- Function + F12 puts the laptop to sleep
- Keyboard brightness is function + plus/minus keys on the num pad

### USB Ports 
- HS03 USB2 <-- Top left USB2 port
- HS04 USB2 <-- Bottom left USB2 port
- HS05 TypeC+Sw <-- Orientation 1
- HS06 TypeC+Sw <-- Orientation 2
- HS07 Internal <-- MSI EPF USB, I think this might be the webcam
- HS08 USB2 <-- Right USB
- HS10 Internal <-- BCM2045A0 Bluetooth USB Port
- HS12 Internal <-- USB2.0-CRW SD Card Reader
- SS02 USB3 <-- Bottom left USB3 port*******--
- SS03 USB3 <-- Top left USB3 port
- SS05 TypeC+Sw <-- Orientation 1
- SS06 TypeC+Sw <-- Orientation 2

### Installing Windows 10 and Ubuntu
I finally got around to installing Windows 10 and Ubuntu on my machine, but not without some bumps along the way. I found I struggled with getting Clover to show up after installing these OSs, so I thought I'd give a quick process rundown. I'm not going to get into details of the installs, just the process for swapping drives etc. You'll want to have prepared an Windows 10 installer USB, an Ubuntu installer USB and have a functioning Clover USB on hand.
- Disassemble the bottom and pull out the m2 SSD drive. You'll want to install on the secondary SSHD drive. I already had this partitioned, so I just installed Windows 10 on a new NTFS partition. Put the bottom back on without putting all the screws back in. This laptop isn't the easiest to pull things in and out, so waiting until the end for all the screws saves a lot of headache.
- Create a Windows 10 USB installer and boot with it. Install Windows on the NTFS drive and do any subsequent restarts until Windows is setup, I think it took me 3.
- Create an Ubuntu 19.04 USB installer and boot with it. Create an ext4 partition and set the mount point to /. One restart and Ubuntu should be good to go. You may need a Clover USB to act as bootloader at this point, as it will have installed the Grub Bootloader on the drive.
- Next you'll want to pull the SSHD that you just installed Windows and Ubuntu onto and reinsert the m2 SSD. At this point I found my drive didn't seem to to recognize the Clover EFI setting, so I used my Clover USB to boot up macOS. Mount the EFI partition(however you're used to doing that), then open the /EFI folder. Add underscores to the front of Microsoft and ubuntu folders, which will disable them. Save and restart.
- on restart hit delete and enter the BIOS settings. Under Boot, Hard Drive boot priority(should be the last item on that page) choose UEFI OS (USUALLY NAME OF DRIVE MODEL HERE), and not Ubuntu or Windows Boot Manager. Save and restart. This should now get you booting into Clover off the m2 drive as expected. Shutdown after verifying Clover loaded.
- Go back into your EFI folder and remove the underscores from the Windows and Ubuntu folders
- Now you'll want to reinstall the SSHD drive. Pop it back in and verify you can boot into Windows 10 and Ubuntu. Once you've done that, you're good to reinsert all 16 screws on the back.

### Fixing The Boot Entries in Windows
I run into this problem every so often where my BIOS loses the boot entry for Clover and will only boot into Windows. To fix this I've figured out a process invloving a couple tools, [MiniTool Partition Wizard Free](https://www.partitionwizard.com/free-partition-manager.html) and [BootIce](https://www.softpedia.com/get/System/Boot-Manager-Disk/Bootice.shtml).
- Once you've downloaded and installed Partition Wizard, go into Partition Management and right click the relevant EFI drive( it'll be the 200 MB partition listed first on your drive). From the menu, choose Change Letter and assign the EFI to an unused drive letter. 
- Then open BootIce and go to the UEFI tab and click the Edit boot entries button.
- Click add and open the EFI drive you just mapped and navigate to \EFI\CLOVER\CLOVERX64.efi and click open
- Rename your entry and click Save current boot entry.
- Then move the new boot entry to the top of the list and click close. 
