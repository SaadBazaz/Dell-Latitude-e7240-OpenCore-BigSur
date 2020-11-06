## OpenCore for Lenovo y50-70 updated for Big Sur with BCM94352Z wifi support



**OpenCore - post-installation: 0.6.1**

**Specs:**
  - Intel Core i5-4210H -- [Product Page](https://ark.intel.com/content/www/us/en/ark/products/78930/intel-core-i7-4710hq-processor-6m-cache-up-to-3-50-ghz.html)
  - Intel HD4600 iGPU
  - Nvidia GTX 860M 4GB (unsupported)
  - 12GB DDR3 Ram
  - Broadcom BCM94352Z



**What you need:**

- Lenovo Y50-70 (or Y70 Haswell) with either 1080p or UHD/4K display
- macOS or OS X downloaded from the Mac App Store
- 8GB USB stick with EFI folder pre-installation on EFI Partition and MacOSX installation.
- Broadcom BCM94352Z for native WiFi (Lenovo FRU: 04X6020, Lenovo PN: 20-200480) or MacOS Broadcom compatible model with BIOS unlock.

**What works:**

Expect to work:
- built-in keyboard (with brightness keys)
- built-in trackpad (multi gestures)
- HDMI video/audio with hotplug
- AirPlay mirroring to AppleTV
- native WiFi via BCM94352Z
- Bluetooth (with handoff) using BCM94352Z
- native USB3
- native audio with AppleHDA
- built-in mic
- built-in camera
- native power management
- battery status
- backlight controls with smooth transitions, save/restore across restart
- accelerated graphics for HD4600 including OpenCL
- wired Ethernet
- retina scaling (in the case of UHD screen)

**Not working:**

- Nvidia GTX 860M 4GB (It doesn't work and it will never work)
- card reader 


**BIOS settings:**

To start, set BIOS to Windows 8 defaults.

Then insure:
- UEFI boot is enabled
- secure boot is disabled
- enable Legacy Boot (but UEFI first) and you may experience less boot time glitches

**For the UHD model, the DVMT-prealloc BIOS setting must be changed to 128MB. One of two methods can be used:**
- use a EFI shell to change the DVMT-prealloc from the shell.
- use a patched BIOS which unlocks the advanced menu

# What you have to do:
 
- Install MacOS with pre-installation EFI

- copy EFI post-installation folder on EFI partition of your HD.

- Modify SMBIOS data with your information for imessage/facetime

(You have to import from your older configuration or generate a new one)
  
    - Use MacSerial to generate your SMBIOS --[Macserial](https://github.com/acidanthera/OpenCorePkg/tree/master/Utilities/macserial)
    - MacSerial Example in terminal macserial -a | grep -i iMac19,1

Output Example from above command:

- iMac19,1 | C02YC2Y1JV3Q | C02909403CDLNV9A8 
- iMac19,1 | C02YX1Y9JV3Q | C02926401GULNV91H
- iMac19,1 | C02YN07JJV3Q | C02918207J9LNV91M
- iMac19,1 | C02YJKZTJV3Q | C029142004NLNV9A8
- iMac19,1 | C02Y6QY5JV3Q | C02905100CDLNV9FB
- iMac19,1 | C02Z4EY6JV3Q | C02930310GULNV98C
- iMac19,1 | C02Y1VY1JV3Q | C02853130GULNV91M
- iMac19,1 | C02ZL06PJV3Q | C029438024NLNV9JA
- iMac19,1 | C02YX072JV3Q | C02926500CDLNV9CB
- iMac19,1 | C02ZW3YFJV3Q | C02952301GULNV9UE


Generic:

    SpoofVendor: YES (This prevents issues with having “Apple,inc” as manufacturer).
    SystemUUID: Can be generated with MacSerial or use previous from Clover’s config.plist.
    MLB: Can be generated with MacSerial or use previous from Clover’s config.plist.
    ROM: <> (6 character MAC address, can be entirely random but should be unique).
    SystemProductName: Can be generated with MacSerial or use previous from Clover’s config.plist.
    SystemSerialNumber: Can be generated with MacSerial or use previous from Clover’s config.plist.
    

  
Data that you have to modify on Config.plist/Platforminfo/Generic with [PlistEditorPro](https://www.fatcatsoftware.com/plisteditpro/) or other plist editor.
  
  ![PliseditorPRO](https://raw.githubusercontent.com/SaxMachine/Lenovo-Y50-70-OpenCore/master/1.png)
  
  
**Post installation commands to do**

- sudo pmset -a hibernatemode 0
- sudo rm /var/vm/sleepimage
- sudo mkdir /var/vm/sleepimage

**Credits:**

*Rehabman
[tonymacx86 forum](https://www.tonymacx86.com/threads/guide-lenovo-y50-uhd-or-1080p-using-clover-uefi.261723/)


*Xsiry
[Github xsiry](https://github.com/xsiry/Lenovo-Y50-Hackintosh-OC/)

*acidadanthera
[Github Acidanthera](https://github.com/acidanthera/OpenCorePkg)

*macos86.it
[Forum](https://www.macos86.it)
