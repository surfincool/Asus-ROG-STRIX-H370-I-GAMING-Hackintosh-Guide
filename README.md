![Banner](https://raw.githubusercontent.com/Autocrit/Asus-ROG-STRIX-H370-I-GAMING-Hackintosh-Guide/master/images/banner4.jpg "Banner")

# Asus ROG STRIX H370-I GAMING Hackintosh Guide

## October 2020 switch to OpenCore
The old version of this guide, using Clover and *CorpNewt's [Hackintosh Vanilla Desktop Guide](https://hackintosh.gitbook.io/-r-hackintosh-vanilla-desktop-guide/)* can be found [*here*](README_OLD.md). I had started to get regular graphics (I think) - related lock-ups (i.e. black screen/force shutdown) with the Clover-based install, and updating Clover and kexts had become complicated. So far there have been no lock-ups with OpenCore. 

## My system
* CPU: Intel Core i7-8700K
* CPU cooler: Noctua NH-L9i chromax.black
* Motherboard: Asus ROG Strix H370-I Gaming
* Memory: Corsair Vengeance LPX 16 GB (2 x 8 GB) DDR4-3200
* Storage: 2 x Samsung 970 Evo Plus 500 GB M.2-2280 NVME Solid State Drive
* Video card: PowerColor Radeon RX 5700 XT 8 GB Red Dragon
* Case: DAN Cases A4-SFXv4.1
* Power supply: Corsair SF 600W 80+ Platinum

## OpenCore guide
I followed the [*Dortania*](https://dortania.github.io/OpenCore-Install-Guide/) guide step-by-step; as I'm new to OpenCore I'll only add a few comments.

## ACPI
I ran SSDTTime in Windows with the following options:
- Dump DSDT
- FakeEC
- PluginType
- PMC
- AWAC

Then added:
- SSDT-USBX.aml

## PlatformInfo
I'm using an *iMac19,1* SMBIOS

## USB 15 port limit
![USBMap](https://raw.githubusercontent.com/Autocrit/Asus-ROG-STRIX-H370-I-GAMING-Hackintosh-Guide/master/images/usb_map.png "USBMap")
- although the cleaner method is probably to generate a USBMap.kext with USBMap, I'm still using USBInjectAll.kext, XHCI-unsupported.kext and SSDT-UIAC.aml generated previously
- this graphic might still be useful when deciding which ports to include or exlude:
![Asus H370-I GAMING USB ports](https://raw.githubusercontent.com/Autocrit/Asus-ROG-STRIX-H370-I-GAMING-Hackintosh-Guide/master/images/asus-h370-i-gaming-usb-ports-2.png "Asus H370-I GAMING USB ports")
- example [SSDT-UIAC.dsl](https://github.com/Autocrit/Asus-ROG-STRIX-H370-I-GAMING-Hackintosh-Guide/blob/master/resources/SSDT-UIAC.dsl) with unused/excluded ports commented out

## Audio
- my layout id is 7, so I have this in DeviceProperies:
```
<key>PciRoot(0x0)/Pci(0x1F,0x3)</key>
<dict>
	<key>layout-id</key>
	<data>BwAAAA==</data>
</dict>
```

## Issues
### RTC/CMOS error
- on restart I was getting the BIOS error "The system has posted in safe mode". This is fxed with *DisableRtcChecksum* in Kernal->Quirks set to *true*

### OpenCore GUI
> - this isn't working at the moment and I'm not sure why
- updating to OpenCore 0.6.3 (with the necessary driver, kext and config.plist updates) has fixed this so the GUI is now working.

### Windows 10
- wake from sleep in Windows 10 is broken since the move to OpenCore

![Big Sur](https://raw.githubusercontent.com/Autocrit/Asus-ROG-STRIX-H370-I-GAMING-Hackintosh-Guide/master/images/big_sur_banner.jpg "Big Sur")
