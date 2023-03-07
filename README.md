# Acer-Aspire-A515-55-38L9

### THIS IS AN UPDATE OF THE EFI FROM hanlywijaya (https://github.com/hanlywijaya/Acer-Aspire-A515-55-Opencore) ###

### **I am not responsible for any damage or if your computer turns into a lemon all of a sudden. Everything you do is not guaranteed to work & you are responsible.**
### **PLEASE READ THE WHOLE README FILE TO UNDERSTAND WHAT TO DO FOR THIS EFI.**

At this moment, **it's only developed for macOS Big Sur**, maybe in the future I update it for Mojave or later.

### ¡Important info!
- Please add `SystemSerialNumber`, `SystemUUID` and `MLB`, along with updating some BIOS settings listed below.
- My laptop came with the Qualcomm WiFi card, so the wifi isn't working, as a replacement I installed the driver for tethering through android.
- When I start the computer on the login section, the screen starts acting crazy for around 5 seconds and then turns back to normal (you can skip this strange error just by start typing the password).
- There's no Mac with the UHD Graphics G1, so in order to make everything work I change the Device ID so that macOS thinks the computer has an Intel Iris Plus Graphics card (GPU Device ID: 0x8A5C8086), this is not an optimal option, but is the only way I found out to make the OS usable.
- I haven't tested installing macOS on a nVME disk, so I'm not 100% sure it'll work, but I thing everything will be fine.


I recommend if you are using a different type of CPU model, to follow the Opencore guide on fixing up the configuration plist to be built for your Mac. You may want to use my EFI as a template for everything you need. - https://dortania.github.io/OpenCore-Install-Guide/

### BIOS Settings
* *Security* → Set supervisor password (to disable secure boot)
* *Security* → Password on boot → **Disable**
* *Boot* → Secure Boot → **Disable**
* *Boot* → Boot Mode → **UEFI**
* *Main* → Lid Open resume → **Enabled**

### Tested

- [x] Internal Audio and Headphone Jack
- [x] iGPU Acceleration
- [x] Battery Readings
- [x] Ethernet
- [ ] Wifi + Bluetooth
- [x] Display Brightness Control
- [ ] Sleep Functionality (you can use lid open and sleep as a alternative)
- [x] Lid Close and Open (semi-working)
- [x] USB ports (3.0, 2.0 & USB-C)
- [x] Webcam
- [x] Trackpad with multi finger gestures 
- [ ] HDMI (you can use AirPlay/USB-C to HDMI as a alternative)
- [x] Native hotkey support with Fn keys
- [x] Tethering for android (as a temporal replace of the Wi-Fi card)

### Specs for tested Aspire 5:
- 1.20ghz Intel Core i3-1005G1 (Ice Lake)
- 12GB RAM
- Intel UHD Graphics G1 (iGPU)
- Realtek ALC255 (using layout 30 for AppleALC)
- Qualcomm QCA6174 802.11ac Wireless Network Adapter

### SMBIOS used for my model (recommended to follow guide link in **What is needed to be changed**)
MacBookAir9,1

### BIOS Settings
* *Security* → Set supervisor password (to disable secure boot)
* *Security* → Password on boot → **Disable**
* *Boot* → Secure Boot → **Disable**
* *Boot* → Boot Mode → **UEFI**
* *Main* → Lid Open resume → **Enabled**

### Guide
This guide will help you from the start to the end : [Dortania Gitbook](https://dortania.github.io/OpenCore-Install-Guide/)
Generating Serial Number : GenSMBIOS from Corpnewt [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS)

### How to install/upgrade EFI
For installing macOS, put the EFI in the EFI partition. To mount the EFI partition, go to Terminal, and type 'diskutil list'. It should show a list of disks and one of the disks should be the installer (should have the same name as the USB you will be using for installing' and a partition in the list with the installer named 'EFI'. Do not choose disk0s1 (main disk) or disk1s1 (if you have a second disk installed) and find for example, disk2s1. There should be a identifier for example, 'disk3s1'. You want to type 'sudo diskutil mount diskidentifier' then type your password to mount the EFI. After proceeding, you will need to change your model idenifier, serial number, ROM & MLB for iCloud, iMessage & FaceTime to function, along with being able to install and boot macOS. You can place a copy of the latest EFI from the GitHub repo and make sure you have replaced the wordings for model identifier, serial number & ROM have been replaced. I recommend using Opencore Configurator as it is easy to use for most users. Go to PlatformInfo and the first tab in Opencore Configurator and replace all the placeholder texts, I recommend using the guide for easier instructions. (https://dortania.github.io/OpenCore-Post-Install/universal/iservices.html#using-gensmbios) 

For upgrading your EFI, you simply only need to follow all the steps and use the same serial number, model identifier, etc in the config.plist file for the newest EFI. Do not replace your SMBIOS (serial number, model identifier, etc) if you are still logged into iCloud. If you want to change your SMBIOS, you will need to log out of iCloud & other Apple services to be able to swap your SMBIOS without issues.


###  Basic Installation

- Create a Bootable USB for MacOS by using by Dortania's [OpenCore-Install-Guide](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/).
- Install MacOS to SSD / Hard drive. (While installing, connect USB keyboard and mouse).
- Copy **ALL** the Contains of this Repo inside the EFI partition of SSD / Hard drive.
- **[IMPORTANT]** Make sure to Generate system definitions of MacBookAir9,1 (for those who use 10th gen Intel/Ice Lake) in config.plist file using [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS) & add `SystemSerialNumber`, `SystemUUID` and `MLB`.

### Post Installation
- If you have Installed MacOS on SSD, Enable TRIM using following command:

```sh
$ sudo trimforce enable
```
