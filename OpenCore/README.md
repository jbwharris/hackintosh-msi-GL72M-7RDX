#  MSI GL72M 7RDX Hackintosh Laptop

This is an OpenCore install for MacOS Mojave 10.15.3. This build is now a triple boot, Mojave, Windows 10 and Ubuntu build.

### MSI GL72M 7RDX Laptop Specs
- Core i7 7700HQ
- Intel HD 630
- GeForce® GTX 1050 with 2GB GDDR5
- Intel® HM175 chipset
- Realtek ALC898
- 17.3" HD display 1920x1080
- 16gb 2400mhz DDR4
- 250GB WD Blue 3D NAND PC SSD
- 1TB ADATA SU800 SSD
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

### 1TB ADATA SU800 SSD
Windows and Ubuntu run off this drive, as well as a clone of the main SSD.

## BIOS Configuration
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

## Installation Notes

### USB Port Limit 
I used Hackintool to fix my USB ports, along with a few other issues. It generated a new USBPorts.kext for my system and installed it in kexts/other

### Fixing the framebuffer
This has been the bane of my existence when it comes to this laptop. I finally got it working with OpenCore after ages of messing around with Hackintool patches, Skylake spoofs(that previously worked in Clover) and other people's MSI laptop setups. After recently learning how to access the BIOS settings to change the DVMT Pre-Allocated to 64m, which then allowed me to remove the 32mb DVMT-prealloc patches. Then after much trial and error, instead of using the [2 Intel HD Graphics 630 listed under Kaby Lake in the laptop guide](https://dortania.github.io/oc-laptop-guide/prepare-install-macos/display-configuration.html), I tried the Unlisted GPU mentioned right below them and now the LVDS screen no longer has a flicker. 

## Outstanding Issues

### Frontend Cleanup
Need to add a prettier boot screen and remove the debug kexts. 

### SD Card Reader
I have a feeling this might actually work, just haven't tried yet.

### HDMI Audio 
Still haven't had the time to really test this one, just know it doesn't work currently.

## Useful Resource Links
- [Vanilla Laptop Guide](https://dortania.github.io/oc-laptop-guide/)
- [MSI GP62 Hackintosh by Chuxubank](https://github.com/chuxubank/MSI-GP62-Hackintosh)

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
