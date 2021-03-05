# GIGABYTE-Z590-VISION-G-HACKINTOSH-OPENCORE-iGPU-with-dGPU-UHD630-RX580
Opencore Hackintosh settings for Gigabyte Z590 Vision-G


## Components

- M/B: GIGABYTE Z590 Vision-G(BIOS F2)
- CPU: Intel® Core™ i7-10700K Processor
- iGPU: Intel® UHD Graphics 630
- dGPU: SAPPHIRE NITRO AMD Radeon RX 580 4GB
- Ethernet: Intel® i225-V, 2.5 x Gigabit LAN Controller
- WiFi/Bluetooth: BCM94360CS2
- Audio: Realtek® ALC 4080 High Definition Audio
- Case: Fractal Design R7 Compact

## Comments

This Hackintosh build guide is NOT GUARANTEE 100% fully working in your conditions.

This guide has been tested on MacOS Bigsur 11.2.2, OPENCORE 0.6.7 and prefers the use of an AMD dGPU for ease of installation. However, until now, I have NOT found the BEST SETTINGS for iGPU hardware full acceleration.

And this guide can be used on the Gigabyte, MSI, AsRock M/B also. (some settings are different)

## Procedure

1. Install MacOS 11.2.2 or newer(with OPENCORE 0.6.6 or newer)
2. Set the SMBIOS to iMac 20,1 or iMacPro 1,1
3. Apply custom USB Port map files. iMac20,1 and iMacPro1,1 is not matter(USBPorts.kext modified by dhckdgjs) There are 2 ways you can do this:
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

- ITE Device (0x5702 device on USB HS13 port): if you need the RGB Fusion feature, please check other thread as below.
[https://www.tonymacx86.com/threads/gigabyte-z490-vision-d-thunderbolt-3-i5-10400-amd-rx-580.298642/page-24#post-2138475](https://www.tonymacx86.com/threads/gigabyte-z490-vision-d-thunderbolt-3-i5-10400-amd-rx-580.298642/page-24#post-2138475)

## What Works

- Continuity features
- WiFi and BT
- Built-in Ethernet, Audio
- Sleep and wake
- DRM(like Netflix, but only SMBIOS iMacPro1,1)

## What doesn't works

- iGPU hardware acceleration(Quicksync)

## Summary

As far as I have been able to test, everything works well except iGPU hardware acceleration and Thunderbolt devices.(I don’t have ThunderboltEX 3 or Titan/Alpine ridge add-on card)

If you need more detailed settings fot this GIGABYTE Z590 Vision-G M/B, please check released file.(like as USB ports map)

Thanks.

## Screenshots
