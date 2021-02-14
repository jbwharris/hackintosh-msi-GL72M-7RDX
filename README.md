<img src="https://raw.githubusercontent.com/acidanthera/OpenCorePkg/master/Docs/Logos/OpenCore_with_text_Small.png" width="200" height="48"/>

#  MSI GL72M 7RDX ( Also work GL62M 7RDX ) Hackintosh Laptop

This is an OpenCore 0.6.6 install for MacOS Big Sur 11.2 . 

This build is only for Big Sur, Windows 10 -> BOSD .

<img src ="https://raw.githubusercontent.com/vincent-chang-rightfighter/hackintosh-msi-GL72M-7RDX/Bigsur_OC_0.6.6/screenshots/About.png" width="700" />

### MSI GL72M 7RDX Laptop 
| :computer: Specifications | :thumbsup: Functioning Components | :no_entry: Non-Functioning Components |
|--|--|--|
| Intel HD 630 | :white_check_mark: Intel HD 630 1536mb working | :x: nVidia GTX 1050 |
| GeForce® GTX 1050 with 2GB GDDR5 | :white_check_mark: Wifi | :x: SD card reader |
| Intel® HM175 chipset | :white_check_mark: USB C/3.0 | |
| Realtek ALC898 | :white_check_mark: Ethernet port | |
| 17.3" HD display 1920x1080 | :white_check_mark: Audio | |  
| 16gb 2400mhz DDR4 | :white_check_mark: Microphone | |
| 250GB WD Blue 3D NAND PC SSD | :white_check_mark: iMessage/Facetime | |
| 1TB ADATA SU800 SSD | :white_check_mark: Sleep/Wake functionality | |
| Broadcom DW1820A BCM94350ZAE  | :white_check_mark: Keyboard brightness | |
| Core i7 7700HQ | :white_check_mark: Screen brightness adjustment | |
| Backlight Keyboard (Single-Color, Red) | :white_check_mark: Webcam | |
| HDMI | :white_check_mark: HDMI | |
| Mini Display Port | :white_check_mark: Mini Display Port | |
|[Manufacturers Website](https://www.msi.com/Laptop/GL72M-7RDX/Specification) | :white_check_mark: Ethernet through USB C | |

### MSI GL62M 7RDX Laptop 
| :computer: Specifications | :thumbsup: Functioning Components | :no_entry: Non-Functioning Components |
|--|--|--|
| Intel HD 630 | :white_check_mark: Intel HD 630 1536mb working | :x: nVidia GTX 1050 |
| GeForce® GTX 1050 with 2GB GDDR5 | :white_check_mark: Wifi | :x: SD card reader |
| Intel® HM175 chipset | :white_check_mark: USB C/3.0 | |
| Realtek ALC898 | :white_check_mark: Ethernet port | |
| 15.6" HD display 1920x1080 | :white_check_mark: Audio | |  
| DDR4 2400mhz 8gb * 2  | :white_check_mark: Microphone | |
| Samsung 860 Evo 500GB SSD | :white_check_mark: iMessage/Facetime | |
| 512GB ADATA SU800 SSD | :white_check_mark: Sleep/Wake functionality | |
| Broadcom DW1820A BCM94350ZAE  | :white_check_mark: Keyboard brightness | |
| Core i7 7700HQ | :white_check_mark: Screen brightness adjustment | |
| Backlight Keyboard (Single-Color, Red) | :white_check_mark: Webcam | |
| HDMI | :white_check_mark: HDMI | |
| Mini Display Port | :white_check_mark: Mini Display Port | |
|[Manufacturers Website](https://www.msi.com/Laptop/GL62M-7RDX/Specification) | :white_check_mark: Ethernet through USB C | |

## :muscle: Upgrades

### Wifi Card
I purchased a Broadcom DW1820A BCM94350ZAE 2.4G/5G Dual Band 867Mbps M.2 NGFF WiFi Card with Bluetooth 4.1 and swapped it into the laptop. 

### USB C Hub
Hub works and allows me to plugin additional USB items and read SD cards, but HDMI passthrough do not work. The ethernet connection does work, so I can just plugin the hub and be connected to a wired connection automatically.

### Samsung 860 Evo 500GB SSD - SATA III 6 Gb/s 2.5 Inch Solid State Drive
Main boot drive for this machine.

### 512GB ADATA SU800 SSD - SATA III 6 Gb/s M.2 2280 Solid State Drive
Windows run off this drive.

## :older_man: BIOS Configuration
The section below adapted from @0ranko0P's [MSI-GL62M 7RD Hackintosh](https://github.com/0ranko0P/GL62M-7RD-Hackintosh/blob/OC_Catalina_DW1820A/README.md). 
~~This was huge, as I never knew how to access all the advanced settings in my BIOS.~~

**Some options only available in advanced mode:**\
In BIOS, holding **Right Shift + Right Ctrl + Left Alt** together then press **F2**

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

## :notebook_with_decorative_cover: Installation Notes

### ACPI Patching Notes
This laptop already has an embedded controller named EC in the DSDT, so it doesn't need to be patched.

### USB Port Limit 
I used Hackintool to fix my USB ports, along with a few other issues. It generated a new USBPorts.kext for my system and installed it in kexts/other. This iteration removes the MSI EPF USB and USB2.0-CRW SD Card Reader, as they serve no purpose.  

### Fix HD 630 issue

~~This has been the bane of my existence when it comes to this laptop. I finally got it working with OpenCore after ages of messing around with Hackintool patches, Skylake spoofs(that previously worked in Clover) and other people's MSI laptop setups. After recently learning how to access the BIOS settings to change the DVMT Pre-Allocated to 64m, which then allowed me to remove the 32mb DVMT-prealloc patches. Then after much trial and error, instead of using the [2 Intel HD Graphics 630 listed under Kaby Lake in the laptop guide](https://dortania.github.io/oc-laptop-guide/prepare-install-macos/display-configuration.html), I tried the Unlisted GPU `05001c59` mentioned right below them and now the LVDS screen no longer has a flicker.~~

Fix with 

```
<key>PciRoot(0x0)/Pci(0x2,0x0)</key>
			<dict>
				<key>AAPL,ig-platform-id</key>
				<data>AAAbWQ==</data>
				<key>AAPL,slot-name</key>
				<string>Internal@0,2,0</string>
				<key>device-id</key>
				<data>G1kAAA==</data>
				<key>device_type</key>
				<string>VGA compatible controller</string>
				<key>disable-external-gpu</key>
				<data>AQAAAA==</data>
				<key>enable-hdmi20</key>
				<data>AQAAAA==</data>
				<key>framebuffer-con2-enable</key>
				<data>AQAAAA==</data>
				<key>framebuffer-con2-index</key>
				<data>/////w==</data>
				<key>framebuffer-con2-type</key>
				<data>AAgAAA==</data>
				<key>framebuffer-fbmem</key>
				<data>AACQAA==</data>
				<key>framebuffer-patch-enable</key>
				<data>AQAAAA==</data>
				<key>framebuffer-portcount</key>
				<data>AgAAAA==</data>
				<key>framebuffer-stolenmem</key>
				<data>AAAwAQ==</data>
				<key>hda-gfx</key>
				<string>onboard-1</string>
				<key>model</key>
				<string>Intel HD Graphics 630</string>
			</dict>
```


### Bluetooth using DW1820A BCM94350ZAE
I have struggled for a long time with getting the Bluetooth to work on this laptop. The thing that finally worked for me was adding 'bpr_probedelay=200 bpr_initialdelay=400 bpr_postresetdelay=400' to my boot-args. [Revised solutions to DW1820A support](https://github.com/osy86/HaC-Mini/issues/243)

### Wifi using DW1820A BCM94350ZAE on Big Sur
After getting Big Sur to work on my machine the biggest issue was getting the wifi to actually work. I had to set a boot-arg to `brcmfx-driver=2` and change the entry in for AirPortBrcm4360_Injector.kext to MaxKernel 19.9.9. That's all in the OpenCore Guide, but thought it worth flagging. 

### Getting the touchpad and buttons to function
[@kOOsi3](https://github.com/jbwharris/hackintosh-msi-GL72M-7RDX/issues/10#issuecomment-678415267) pointed out a solution to getting the touchpad to work. I just had to use an older Rehabman kext instead of the latest version. 

## :man_facepalming: Outstanding Issues

### Flat audio through USB 
I've noticed this issue lately where the audio coming through the USB C hub to my Creative speakers is really flat sounding. Then when the laptop screen goes to sleep, it'll go back to sounding good, then when woken up it's flat again. When connected via Bluetooth it sounds great, but then I can't actually push audio out to it at the same time as my Airplay speakers. Still trying to figure out an ideal solution there. 


## Useful Info
- [Vanilla Laptop Guide](https://dortania.github.io/OpenCore-Install-Guide/)
- [MSI GP62 Hackintosh by Chuxubank](https://github.com/chuxubank/MSI-GP62-Hackintosh)
- [Hackintosh--MSIGL62M-7RDX by ForceGT](https://github.com/ForceGT/Hackintosh--MSIGL62M-7RDX)

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

## Add Platforminfo Yourself

<img src="https://raw.githubusercontent.com/vincent-chang-rightfighter/hackintosh-msi-GL72M-7RDX/Bigsur_OC_0.6.6/screenshots/Editinfo.png" width="900"/>

- Serial Number
- UUID
- MLB
- ROM
