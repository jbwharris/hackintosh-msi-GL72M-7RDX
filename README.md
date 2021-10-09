
# Asus X542UQ Catalina Hackintosh
This repository provides you the material of installation the Catalana Hackintosh with Opencore. Here you can find RELEASE and DEBUG versions. Feel free to ask questions and make contributions.

<br>

## ASUS X542UQ Laptop 
| :computer: Specifications | :thumbsup: Functioning Components | :no_entry: Non-Functioning Components |
|--|--|--|
| Intel HD 630 | :white_check_mark: Intel HD 620 1536mb working | :x: nVidia GT 940mx |
| GeForce® GT 940mx with 2GB GDDR5 | :white_check_mark: USB C/3.0 | :x: SD card reader (not tested yet) |
| Realtek ALC294 | :white_check_mark: Ethernet port |  :x: Wifi |
| 15.6" 16:9, 1920 x 1080 pixel 141 PPI, glossy: no | :white_check_mark: Audio | :x: VGA port |  
| 12gb 2133mhz DDR4 (extended) | :white_check_mark: Microphone | |
| 256GB Apacer AS350 PANTHER  SSD | :white_check_mark: iMessage/Facetime | |
| Qualcomm Atheros QCA9377 Wireless Network Adapter | :white_check_mark: HDMI | |
| Core i3 7100U | :white_check_mark: Screen brightness adjustment | |
| PS/2 Keyboard | :white_check_mark: Webcam | |
| I2C ELAN1200 Trackpad | :white_check_mark: Sleep/Wake functionality | |
| HDMI | | |
|[Manufacturers Website](https://www.asus.com/ru/Laptops/For-Home/VivoBook/ASUS-VivoBook-15-X542UQ/) | | |

## :muscle: Upgrades

### Wifi Card
You need to purchase a Broadcom DW1820A BCM94350ZAE 2.4G/5G Dual Band 867Mbps M.2 NGFF WiFi Card with Bluetooth 4.1 (for example or other wifi adapter for "naive" work) for correctly working wifi. 

### 256GB Apacer AS350 PANTHER  SSD
Main boot drive for this machine.

## :older_man: BIOS Configuration
I use the latest version of bios - 309. You can update bios [here](https://www.asus.com/supportonly/X542UQ/HelpDesk_BIOS/). <br> For installation without any troubles you need to edit some setting in bios that provided below

| Settings |  |
|--|--|
| CSM | Disable |
| Fast Boot | Disable |
| Secure Boot | Disable |
| Intel Virtualization Technology | Disable |
| Enable Hiberation | Disable |
| VT-D | Disable |
| Wake on Lan | Disable |
| Legacy USB support | Enabled |
| DVMT Pre-Allocated | 64M |

After installation you can Intel Virtualization Technology and VT-D Enable for working with virtual mahines.

## :notebook_with_decorative_cover: Installation Notes

### Installation of Catalina by using this repository
If you want to install it quick - you can download DEBUG or RELEASE version, create the boot flash [(see more)](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/) and copy DEBUG or RELEASE EFI folder into mounted EFI partition (on your flash). In config.plist there are already generated serial numbers, but its better to change them using the [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS). `Attenton!` The eGPU is disabled via [IORegistryExplorer](https://github.com/acidanthera/gfxutil/releases), [guide](https://dortania.github.io/OpenCore-Install-Guide/extras/spoof.html).

### USB Port Limit 
I used USBMap to fix my USB ports, along with a few other issues. It generated a new USBPorts.kext for my system and installed it in kexts/other. If you want to generate it by yourself you can use this tool and guide - [USBMapping Guide By Dortania](https://dortania.github.io/OpenCore-Post-Install/usb/intel-mapping/intel.html).


### Wifi using 
If you want wifi to work you need to buy Broadcom DW1820A BCM94350ZAE module. If you have an Wi-Fi usb adapter here is a guide for you [Wireless USB Adapter](https://github.com/chris1111/Wireless-USB-OC-Big-Sur-Adapter). Be carefully with kext after installation, because in my case it did not worked untill i swapped RtWlanU.kext and RtWlanU1827.kext loading priorities in the config.plist.

### Getting the touchpad and buttons to function
In the kext folder there are 2 kexts for I2C touchpad - VoodooI2C and VoodooI2CHID. Due to I have and ELAN1200 version of touchpad this protocol needs to use VoodooI2CHID. But I have only one problem - in some programs or workspaces (like Desktop) left button behaves like right button (cant drag and files).

### Sleep/Wake functionality problems
This laptop can be taken to sleep correctly without a charger connected to it. If we plug in the AC the laptop will awake in a few seconds after hibernation. This happens due to asus laptops peculiarities. But if you find the solution, feel free to contribute .

## Useful Info
- [Dortania Guide](https://dortania.github.io/OpenCore-Install-Guide/)
- [Wireless USB Adapter](https://github.com/chris1111/Wireless-USB-Adapter-Clover)
- [USBMapping](https://dortania.github.io/OpenCore-Post-Install/usb/intel-mapping/intel.html)
- [Hackintools](https://github.com/headkaze/Hackintool)
