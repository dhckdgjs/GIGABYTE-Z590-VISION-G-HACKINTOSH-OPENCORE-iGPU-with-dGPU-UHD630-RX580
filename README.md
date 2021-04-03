# GIGABYTE-Z590-VISION-G-HACKINTOSH-OPENCORE-iGPU-with-dGPU-UHD630-RX580
Opencore Hackintosh settings for Gigabyte Z590 Vision-G


## Components

- GIGABYTE Z590 Vision-G(BIOS F2 with ALC4080, i225-V)
- Intel® Core™ i7-10700K Processor (10th Gen, UHD630)
- Samsung DDR4 32GB 3200MHz (2 x 16GB)
- 3RSYS RC400 CPU Cooler
- EVGA 750 GQ
- Fractal Design R7 Compact
- LG 43UN700 43-inch UHD Monitor


## Components: Already owned

- Micron MX300 750G
- SAPPHIRE NITRO AMD Radeon RX 580 4GB
- BCM94360CS2 / BT WiFi Card
- Realforce 106U-KB USB Keyboard
- Kensington Slimblade USB Trackball
- Lexar LRW400 Memory Reader
- Sound Blaster Play! 3 USB Sound card


## Caution
GIGABYTE Z590 Vision-G M/B(BIOS F2) CAN NOT BOOT with GIGABYTE RX580 MINING or GAMING.
(Compatibility issue)


## Comments

This Hackintosh build guide is NOT GUARANTEE 100% fully working in your conditions.

This guide has been tested on MacOS Bigsur 11.2.2, OPENCORE 0.6.7 and prefers the use of an AMD dGPU for ease of installation. ~~However, until now, I have NOT found the BEST SETTINGS for iGPU hardware full acceleration.~~

And this guide can be used on the Gigabyte, MSI, AsRock M/B also. (some settings are different)

## Procedure

1. Install MacOS 11.2.2 or newer(with OPENCORE 0.6.6 or newer)
2. Set the SMBIOS to iMac20,2 ~~iMac 20,1 or iMacPro 1,1~~
3. Apply custom USB Port map files. ~~iMac20,2, iMac20,1 and iMacPro1,1 is not matter(USBPorts.kext modified by dhckdgjs)~~ There are 2 ways you can do this:
- USBPorts.kext without USBInjectall.kext
- SSDT-UIAC-Z590-VISION-G-V1.aml with USBInjectall.kext

cf) Custom USBInjectall.kext by softxing(for XHC 500 Series USB Chipset 8086:43ed) [https://gitee.com/softxing/OS-X-USB-Inject-All](https://gitee.com/softxing/OS-X-USB-Inject-All)

4. Change M/B Bios Primary display(ASUS) or Initial Display Output(Gigabyte) to PEG or PCIe 1(and iGPU MUST be turned on)
5. Apply the Framebuffer patch(Headless) on your Devices setting in config.plist. (check settings as below and recommend using the Hackintool)

    ```
    AAPL,ig-platform-id: 0300C89B(maybe works well 0x3E920003)

    device-id: C59B0000 Intel UHD 630(maybe works well 0x3E92, 0x3E98 etc., not necessarily)

    igfxfw: 02000000
    ```

    Ref.
    [https://dortania.github.io/OpenCore-Install-Guide/config.plist/comet-lake.html#deviceproperties](https://dortania.github.io/OpenCore-Install-Guide/config.plist/comet-lake.html#deviceproperties)
    [https://github.com/acidanthera/WhateverGreen/blob/master/Manual/FAQ.IntelHD.en.md](https://github.com/acidanthera/WhateverGreen/blob/master/Manual/FAQ.IntelHD.en.md)

6. Built-in Audio (ALC 4080) no need any settings or kexts. ALC 4080 uses USB HS14 port. It looks like External USB Sound Card.
7. Built-in Ethernet (Intel i225-V 2.5GBe controller) only works with fake device-id(F2150000) and FakePCIID.kext, FakePCIID_Intel_I225-V.kext.
Also, I recommend manual hardware configuration in Ethernet advanced settings.

- System will NOT boot without **SSDT-AWAC.aml**
- ITE Device (0x5702 device on USB HS13 port): if you need the RGB Fusion feature, please check other thread as below.
[https://www.tonymacx86.com/threads/gigabyte-z490-vision-d-thunderbolt-3-i5-10400-amd-rx-580.298642/page-24#post-2138475](https://www.tonymacx86.com/threads/gigabyte-z490-vision-d-thunderbolt-3-i5-10400-amd-rx-580.298642/page-24#post-2138475)

## What Works

- Continuity features
- WiFi and BT
- Built-in Ethernet, Audio
- Sleep and wake
- DRM(like Netflix, but only SMBIOS iMacPro1,1)
- FCPX editing, skimming, export
- iGPU Hardware Acceleration(Quicksync)

## What doesn't works

- Nothing
- ~~Sleep and wake works but Fan still running~~ (Fixing USB Ports map settings: USBPorts.kext and SSDT-UIAC-Z590-VISION-G-V2.aml)
- ~~iGPU hardware acceleration(Quicksync)~~


## Summary

As far as I have been able to test, everything works well except ~~iGPU hardware acceleration and~~ Thunderbolt devices.(I don’t have ThunderboltEX 3 or Titan/Alpine ridge add-on card)

If you need more detailed settings fot this GIGABYTE Z590 Vision-G M/B, please check released file.(like as USB ports map)

Thanks.


## Update 21.04.04
Fix USB Ports map settings.(Sleep and wake work well)
This update affected both ways.(kext and acpi)


## Update 21.03.12
iGPU H/W acceleration works smoothly and quickly.
(SMBIOS iMac20,2 / platform-id 0300923E / device-id 923E0000)

cf. If H/W acceleration doesn't work after MacOS 11.2.3 update, change ID to 0300983E and 983E0000. Please check config.plist ver0.4.


### Sample clip export test

Original: AVCHD(H.264), MOV, 3840*2160, 29.97p(100Mbps), 4:2:0, 8Bit, Long GOP, AAC, 29:54

Export: FCPX 10.5.1, H.264, MP4, 1920*1080, 29.97p(2000kbps), 29:54


- iMac20,2, Bigsur 11.2.2, OC 0.6.7, 10700K, GA Z590 Vision G, RX580: **26:44(This Hackintosh)**
- iMac19,1, Catalina 10.15.6, OC 0.6.0, 9600K, GA H370 Gaming 3, RX580: **27:35**
- iMac19,1, Bigsur 11.1, OC 0.6.7, 9900K, GA Z390 Designare, 9900K, Vega64: **18:12**


**Intel Power Gadget can not show GFX AVG(iGPU). But it works(H/W acceleration) well.**

<img width="300" alt="Screen_Shot_2021-03-09_at_1 21 51_AM" src="https://user-images.githubusercontent.com/35429874/110897783-6d9c3a00-8341-11eb-9c8d-ffb96ac14ba9.png"> <img width="600" alt="Screen_Shot_2021-03-09_at_1 21 54_AM" src="https://user-images.githubusercontent.com/35429874/110897975-c370e200-8341-11eb-818d-d77aede0d87a.png">



## Update 21.03.14

Add some SSDTs(Fake EC Device, SBUS etc.,)


## Screenshots

<img width="1015" alt="Screen Shot 2021-03-05 at 6 17 27 AM" src="https://user-images.githubusercontent.com/35429874/110146164-955d4080-7e1d-11eb-8f91-1459c91b8960.png">
<img width="1097" alt="Screen Shot 2021-03-05 at 6 17 57 AM" src="https://user-images.githubusercontent.com/35429874/110146207-a312c600-7e1d-11eb-906b-97152c15b1ac.png">
ALC 4080 works like External USB Sound Card.
<img width="1015" alt="Screen Shot 2021-03-05 at 6 17 45 AM" src="https://user-images.githubusercontent.com/35429874/110146232-adcd5b00-7e1d-11eb-8e08-3ae945db88db.png">
Intel i225-V 2.5GBe controller works with fake device-id(F2150000) and FakePCIID.kext, FakePCIID_Intel_I225-V.kext.
<img width="1015" alt="Screen Shot 2021-03-05 at 6 17 36 AM" src="https://user-images.githubusercontent.com/35429874/110148669-72805b80-7e20-11eb-9ea7-ed68a106db0a.png">
Manual hardware configuration in Ethernet advanced settings.
<img width="780" alt="Screen Shot 2021-03-06 at 1 03 54 AM" src="https://user-images.githubusercontent.com/35429874/110148507-3cdb7280-7e20-11eb-8aa7-94606d91233a.png">
