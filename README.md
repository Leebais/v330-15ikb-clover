# **v330-15ikb-clover**

## CREDITS

- [OpenIntelWireless](https://github.com/OpenIntelWireless)
- [**[Guide] Lenovo V330-15IKB using Clover UEFI hotpatch**](https://www.tonymacx86.com/threads/guide-lenovo-v330-15ikb-using-clover-uefi-hotpatch.265841/)

## **Overview**	**Can't boot Big Sur**

Welcome to my Lenovo V330-15IKB macOS Mojave guide.
 This laptop is a budget laptop with great upgrade capabilities and excellent macOS compatibility.
 Aside from the small battery and bad display that can be upgrade for a  cheap price this laptop does pack some power and features that not every laptop can fit on such a cheap price while having perfect macOS  compatibility.
 I use Clover UEFI hotpatch method instead of static maciASL patching as  it's the future of hackintosh and allows everyone to use my files  without having to go dump, extract and apply each patch individually  which is a necessary process to be also repeated even if you touched a  single setting on your Bios or hardware change.
 Hotpatch method does not have this problem and offers versatility even  on Bios changes, Hardware Upgrades and small differences that each model of these laptops have between each other.

## **My Laptop Specifications**

- Intel core i5 - 8250U Quad Core CPU (KabyLake R)
- Intel UHD 620 Graphics
- 8GB DDR4 - 2400MHz Ram
- 15.6" Full HD IPS Display (Upgraded)
- ELAN (I2C) TouchPad with Multi-Gestures
- BCM94360CS2 Apple Wireless and Bluetooth Card (Upgraded)
- 2 x USB-C ports & 2 x USB 3.0 Ports
- HDMI & VGA Display Port
- SD Card Reader
- Samsung 850 Pro 256GB 2.5" SSD

### **What works**

- Intel UHD 620 Graphics QE/CI
- USB and USB-C Ports
- Realtek Ethernet
- Audio (All Inputs & Outputs)
- Sleep and Wake
- HDMI and HDMI Audio
- VGA / D-Sub Port
- Dual Band AC Wireless 2.4GHz & 5GHz
- Bluetooth 4.x LE
- CPU and IGPU Power Management
- Battery Status
- Brightness
- Function Keys (Fn)
- I2C ELAN TouchPad with Full Gestures
- Integrated Camera
- SD Card Reader
- Rest of the things that i forgot to list here and that are not listed on "what doesn't work"

### **What doesn't work**

- FingerPrint Reader (3rd Party FingerPrint readers are not supported on macOS, disabled via ACPI)
- AMD Radeon 530 (disabled on ACPI as there's no support for switchable graphics on macOS)

## **What you need**

- Lenovo V330-15IKB Laptop
- macOS Mojave downloaded from the Mac App Store
- 8GB+ USB flash drive
- Downloaded [**v330-15ikb-clover**](https://github.com/Leebais/v330-15ikb-clover) Project from my Github (click on **v330-15ikb-clover**),
- Download as zip like shown below:

## **BIOS**

Before proceeding you need to change some Bios configurations that are necessary for your laptop to work on macOS.
 Press Power button to boot your laptop, as soon as you press it, keep pressing **F2** to enter into Bios Settings.
 Go to **Security** Tab and change settings as listed below:

- Secure Boot **[SetUp Model]**
- Intel SGX **[Can Enable]**
- Intel Platform Trust Technology **[Disabled]**

Now go to **Boot** tab and configure the settings as listed below:

- Boot Mode **[UEFI]**
- USB Boot **[Enabled]**
- PXE Boot to LAN **[Disabled]**

Now go to **Exit** tab:

- OS Optimized Defaults **[Disabled]**
- Exit Saving Changes

Bios configuration completed.

## **Creating USB Installer**

Before proceeding with this guide i would highly suggest that you begin  with a clean install rather than upgrading as the method and kexts are  different than what you might be currently using on your laptop.

**Step 1:**
 Download Clover Bootloader:
https://sourceforge.net/projects/cloverefiboot/

**Step 2:**
 Format USB Drive as HFS+J with GPT partition table and make sure to name it: install_osx

**Step 3:**
 Download macOS Mojave from the Mac App Store, after the download process has finished, now create the USB Installer by opening terminal and  writing the following command:

​		Code: 

```shell
sudo "/Applications/Install macOS Mojave.app/Contents/Resources/createinstallmedia" --volume  /Volumes/install_osx --nointeraction
```



 Press "Enter" and write User and password, hit enter, wait for the process to end which takes around 10-30 minutes.

**Step 4:**
 Download all the needed kexts for "Pre" and "Post" installation which are listed down below.
 They are hyperlinks and should direct you straight to the download page when click on them:

- [Lilu.kext](https://github.com/acidanthera/VirtualSMC/releases)
- [VirtualSMC.kext, SMCProcessor.kext, SMCBatteryManager.kext](https://github.com/acidanthera/VirtualSMC/releases)
- [WhateverGreen.kext](https://github.com/acidanthera/WhateverGreen/releases)
- [VoodooPS2Controller.kext](https://bitbucket.org/RehabMan/os-x-voodoo-ps2-controller/downloads/)
- [VoodooI2C.kext & VodooI2CELAN.kext](https://github.com/alexandred/VoodooI2C/releases)
- [RealtekRTL8111.kext](https://bitbucket.org/RehabMan/os-x-realtek-network/downloads/)
- [AppleALC.kext](https://github.com/acidanthera/AppleALC/releases)
- [CodecCommander.kext](https://bitbucket.org/RehabMan/os-x-eapd-codec-commander/downloads/)
- [FakePCIID.kext & FakePCIID_Broadcom_WiFi.kext](https://bitbucket.org/RehabMan/os-x-fake-pci-id/downloads/) (**Note:** only use it if Wireless card is not being detected !)
- EFICheckDisabler.kext - included on the **Lenovo-V330-15IKB** folder of my Github Repository
- USBPorts.kext - - included on my **Lenovo-V330-15IKB** Github Repository

**Step 5 (Installing Clover Bootloader)**

Of course, you can use my EFI file directly

 Prepare USB Drive with the correct configuration, kexts, Bootloader, config.plist and ACPI
**Note:** if you accidentally install Clover Bootloader into the real iMac, MacMini or MacBook that you are using,
 you might brick it, so be careful and choose the USB drive for installation!

 Install Clover Bootloader by carefully following the steps explained down below:
 Open Clover bootloader installer, click on continue, agree to the terms and conditions, continue,
 Click on "**Change Install Location...**" like shown in the picture below:![Change Install Location-2](/Users/libaoshan/Downloads/Change Install Location-2.png)

Select the USB Flash Drive which in our case is named as "**install_osx**" like shown in the picture below:!![install_osx](/Users/libaoshan/Downloads/install_osx.png)

Click "**Continue**", and now click on the "**Customize**" button like shown in the picture below:![Customize](/Users/libaoshan/Downloads/Customize.png)

At the "**Customize**" section, here we select "**Clover for UEFI booting only**" and "**Install Clover in the ESP**"
Like shown in the picture below:![Installation Type](/Users/libaoshan/Downloads/Installation Type.png)

Now we expand "**UEFI Drivers**" to see the full list of the UEFI Drivers by clicking in the arrow in front of the checkbox and then we select all the UEFI Drivers that we need like i selected them in the picture down below:![UEFI Drivers](/Users/libaoshan/Downloads/UEFI Drivers.png)

Don't select "**Themes**" yet as we will customize that later after we are done with the installation.
Now click Install, it will open a prompt for your Username and Password, write it and press Enter,
the installation will start, after bootloader installation ends, your EFI partition of the USB Drive will be mounted.

## **Preparing USB EFI Partition**

Open the mounted EFI partition of your USB Drive and go to EFI/Clover/
 Replace the **config.plist** with the one from the downloaded **Lenovo-V330-15IKB** repository of my Github
 Into **EFI/Clover/ACPI/Patched** add the **SSDT-V330.aml** from the downloaded **Lenovo-V330-15IKB** Repo
 Into **EFI/Clover/Drivers64UEFI** make sure to add [**HFSPlus.efi**](https://github.com/JrCs/CloverGrowerPro/raw/master/Files/HFSPlus/X64/HFSPlus.efi) (click on **HFSPlus.efi** to download it)
 Into **EFI/Clover/kexts/Others** make sure to add the following kexts listed down below:

- [Lilu.kext](https://github.com/acidanthera/Lilu/releases)
- [VirtualSMC.kext, SMCProcessor.kext, SMCBatteryManager.kext, SMCSuperIO.kext](https://github.com/acidanthera/VirtualSMC/releases)
- [WhateverGreen.kext](https://github.com/acidanthera/WhateverGreen/releases)
- [VoodooPS2Controller.kext](https://bitbucket.org/RehabMan/os-x-voodoo-ps2-controller/downloads/)
- [VoodooI2C.kext & VodooI2CELAN.kext](https://github.com/alexandred/VoodooI2C/releases) - included on my **Lenovo-V330-15IKB** Github Repository
- [RealtekRTL8111.kext](https://bitbucket.org/RehabMan/os-x-realtek-network/downloads/)
- [AppleALC.kext](https://github.com/acidanthera/AppleALC/releases)
- [FakePCIID.kext & FakePCIID_Broadcom_WiFi.kext](https://bitbucket.org/RehabMan/os-x-fake-pci-id/downloads/) (**Note:** only use it if Wireless card is not being detected !)
- [AirportBrcmFixup.kext](https://github.com/acidanthera/AirportBrcmFixup/releases)
- [BT4LEContinuityFixup.kext](https://github.com/acidanthera/BT4LEContinuityFixup/releases)
- EFICheckDisabler.kext - included on the **Lenovo-V330-15IKB** folder of my Github Repository
- USBPorts.kext - - included on my **Lenovo-V330-15IKB** Github Repository

**Step 6:**
 Backup all your important data because we will continue with the installation process on the next step.
 Backup Clover Bootloader installer into the USB Drive for installation (not on the USB EFI folder !)
 Backup my **Lenovo-V330-15IKB** folder download from the Github repository

## **Installation**

**Step 1:**
 Reboot your laptop, after the laptop screen turns on, press **F12** repeatedly to enter into the Boot Menu.
 On the Boot Menu, choose the USB Drive and press "Enter"
 Now it should bring you into the Clover Bootloader menu, select Install macOS Mojave (USB Drive) and press enter.
 The Installer now should boot and reach installation menu.

 **Step 2:**
 From the installation menu, open Disk Utility, select the partition that you plan to install macOS, format it as APFS and for the purpose of  this guide we will name it "Mac". Exit Disk Utility after the format  process has finished, this will bring you back to the Installer Main  Menu.
 Now select install macOS Mojave, agree to the "terms and conditions",  select your HDD/SSD that you formatted and the installation process will begin. this will be the part 1 install. Part 1 should take around 5  minutes.

 **Step 3:**
 Laptop will automatically reboot when Part 1 installation ends. now as  soon as Clover Bootloader menu shows up, this time you select the "Mac"  partition to boot from, the installer will continue with Part 2 now and  show the progress bar with time remaining under the Apple boot logo.
 **Note:** Sometimes as  soon as the time remaining shows up under the Apple boot logo, the  laptop will reboot once more, if this happens, choose again to boot from the "Mac" partition and part 2 installation will continue and complete.
 After the installation has been completed, laptop will reboot and bring you to the part 3 - first boot user setup.

 **Step 4:**
 Select Language, Continue, Connecting to Internet is optional or you can skip it for now.
 When you reach the menu to sign with your Apple ID, make sure to skip  this step, it will be important if you want to setup iMessage &  FaceTime.

## **Post Installation**

**Step 1:**
 Run Apps from anywhere is now missing from SysPrefs > Security & Privacy > General.
 Open terminal and enter the following command:

​		Code: 

```shell
sudo spctl --master-disable
```

This allows you to install Applications downloaded from Internet and outside of the Mac App Store.

**Step 2:**
 Open Clover Bootloader installer and continue with bootloader installation into the HDD/SSD that we installed macOS.
 The procedures are exactly the same as on the Creating USB Installer -  Step 5 of the guide except that this time, instead of the USB Drive, we  select the "Mac" HDD/SSD that we installed macOS.

**Step 3:**
 Now we need to install all the needed kexts into the HDD/SSD where we installed macOS: the "Mac" partition.
 All kexts should be installed into /Library/Extensions

 Download all the kexts if you still didn't:

- [Lilu.kext](https://github.com/acidanthera/Lilu/releases)
- [VirtualSMC.kext, SMCProcessor.kext, SMCBatteryManager.kext](https://github.com/acidanthera/VirtualSMC/releases)
- [WhateverGreen.kext](https://github.com/acidanthera/WhateverGreen/releases)
- [VoodooPS2Controller.kext](https://bitbucket.org/RehabMan/os-x-voodoo-ps2-controller/downloads/)
- [VoodooI2C.kext & VodooI2CELAN.kext](https://github.com/alexandred/VoodooI2C/releases) - included on my **Lenovo-V330-15IKB** Github Repository
- [RealtekRTL8111.kext](https://bitbucket.org/RehabMan/os-x-realtek-network/downloads/)
- [AppleALC.kext](https://github.com/acidanthera/AppleALC/releases)
- [CodecCommander.kext](https://bitbucket.org/RehabMan/os-x-eapd-codec-commander/downloads/)
- [FakePCIID.kext & FakePCIID_Broadcom_WiFi.kext](https://bitbucket.org/RehabMan/os-x-fake-pci-id/downloads/) (**Note:** only use it if Wireless card is not being detected !)
- [AirportBrcmFixup.kext](https://github.com/acidanthera/AirportBrcmFixup/releases)
- [BT4LEContinuityFixup.kext](https://github.com/acidanthera/BT4LEContinuityFixup/releases)
- [BrcmFirmwareRepo.kext](https://bitbucket.org/RehabMan/os-x-brcmpatchram/downloads/)
- [BrcmPatchRam2.kext](https://bitbucket.org/RehabMan/os-x-brcmpatchram/downloads/)
- EFICheckDisabler.kext - included on the **Lenovo-V330-15IKB** folder of my Github Repository
- USBPorts.kext - included on my **Lenovo-V330-15IKB** Github Repository

Extract them and make sure to copy each & only the ones listed above by selecting the "Release" folder of the kexts.
 Create a folder on desktop called "kexts", copy all the listed kexts into that "kexts" folder into desktop
 Open Terminal and write this command to install kexts into /Library/Extensions/

​		Code: 

```shell
cd desktop/kexts

sudo cp -R *.kext /Library/Extensions/
```

Hit enter, write your Username password and all the kexts will be copied and installed into /Library/Extensions/
 Now we need to rebuild caches with the following terminal command:

​		Code: 

```shell
sudo kextcache -i /
```

Wait for the process to end, after the process is completed, reboot.

**Step 4: Disable Hibernation**
 Be aware that hibernation (suspend to disk or S4 sleep) is not supported on hackintosh.

 You should disable it:

​		Code: 

```shell
sudo pmset -a hibernatemode 0
sudo rm /var/vm/sleepimage
sudo mkdir /var/vm/sleepimage
```

Always check your hibernatemode after updates and disable it.  System updates tend to re-enable it, although the trick above (making  sleepimage a directory) tends to help.

 And it may be a good idea to disable the other hibernation related options:

​		Code: 

```shell
sudo pmset -a standby 0
sudo pmset -a autopoweroff 0
```



**Step 5: Install Tools**
 Create a new folder on desktop and name it: tools
 copy patchmatic, iasl, hda-verb and paste them on the "tools" folder that you created on desktop

 Get "**patchmatic**" by clicking on this: [Link](https://bitbucket.org/RehabMan/os-x-maciasl-patchmatic/downloads/RehabMan-patchmatic-2018-0507.zip)
 Get "**iasl**" by click on this: [Link](https://bitbucket.org/RehabMan/acpica/downloads/iasl.zip)
 Get "**hda-verb**" from the CodecCommander folder of the downloaded kext

 Open terminal and write the following commands to install these tools:

​		Code: 

```shell
cd desktop/tools
sudo cp iasl /usr/bin
sudo cp patchmatic /usr/bin
sudo cp hda-verb /usr/bin
```

## **Audio**

For audio we use AppleALC as it has support for "Conexant CX20751/2"  codec using "layout-id 28" which everything is already configured into  the config.plist and the SSDT-V330.aml of my files that you downloaded  from the Github Repo.
 We also need the CodecCommander.kext as it does the correction for  External Microphone (Line-In) and the same fix when the laptop goes into sleep mode and then we wake up the laptop, it keeps the External  Microphone working.

## **Keyboard**

Keyboard is fully mapped and every single button works starting from Brightness to the rest of FN Buttons.
 Fn Buttons do work but you have to assign them as shortcuts on Sysprefs > Keyboard > Shortcuts like my example:

- F4 (Mic On/Off) mapped to Siri shortcut
- F5 (Refresh) available to map as whatever you want
- F6 (TouchPad) Enable and Disable TouchPad
- F7 (Airplane) mapped to Do Not Disturb
- F8 (Camera) mapped to LaunchPad
- F9 (Lock) mapped to System Preferences...
- F10 (Projector) mapped to Video Mirror Toggle
- PrtSc (Print Screen) mapped to Screenshot area of selection or known as the default cmd+4 shortcut

You can customize these keys to something else as you desire on Sysprefs > Keyboard > Shortcuts

## **Touchpad**

For our ELAN (I2C) Touchpad we use Alexandred VoodooI2C.kext and VoodooI2CELAN.kext
 This kext has complete support for our ELAN0618 (9d60) I2C Touchpads and it does support All gestures.
 Some of the gestures are listed down below:

- Pinch to Zoom
- Two Finger Rotation to rotate image left or right
- 2 Fingers scrolling
- 2 Fingers Left Edge swipe
- 2 Fingers Right Edge swipe
- 3 Fingers swipe up
- 3 Fingers swipe down
- 3 Fingers swipe left
- 3 Fingers swipe right
- 3 Fingers Tap (Force Touch)
- 3 Fingers Dragging , etc

**Note:** Some of these laptop models do come with Synaptics I2C Touchpad instead of ELAN I2C Touchpad.
 In that case, instead of using VoodooI2CELAN.kext you need to use VoodooI2CSynaptics.kext

 To fix the "Right Click" physical button on the touchpad, go to **Sysprefs > TrackPad - Point & Click** tab and go to the secondary click and click on the drop down menu and change the current "**Click or tap with two fingers**" selected option to the "**Click in the bottom right corner**" option like shown in the screenshot down below:

## **Wireless and Bluetooth**

Download last released from [**OpenIntelWireless-Factory**](https://github.com/1hbb/OpenIntelWireless-Factory) ,  and follow the steps in this guide to use your intel wireless card.(It's from [**OpenIntelWireless**](https://openintelwireless.github.io))

### itlwm

**`itlwm.kext` uses Apple's IOEthernet rather than IO80211. It is purely based on open-source resources, provides a stabler and faster performance, and the ability to unload on Kernels that use `prelined kernel` mode.**

After you've downloaded our Kernel Extensions from GitHub Release:

1. Unzip
2. Copy the kext files into your Bootloader's kext folder in your EFI partition
3. Make necessary adjustments to your bootloader's config
4. Reboot and enjoy!

### AirportItlwm

**`AirportItlwm.kext` uses Apple's IO80211Family. It provides certain Airport features but lacks stability compared with `AirportItlwm` due to the ambiguity of reverse engineering.**

All steps from `itlwm.kext` + ***one*** of the following steps to load IO80211Family (level of recommendation decreases):

- Enable Apple Secure Boot (**Please read OpenCore's official manual**)
- Force `IO80211Family` to load. 「Supports OpenCore and Clover(not tested)」 (Read the `Kernel - Force` section in OpenCore's manual for more info)
- Load AirportItlwm from Terminal (Continuity features may *not* work)
- Extract IO80211Family from the system, insert AirportItlwm as a Plugin, and load the bundle with a bootloader.
- Disable SIP and install AirportItlwm into `/Library/Extensions` (Take your own risk)



## **iMessage and FaceTime**

This is one of the last steps and things that you should fix after you stabilized your setup in order to properly work.
 For iMessage and FaceTime [@P1LGRIM](https://www.tonymacx86.com/members/374452/) has a step by step detailed guide which you can follow on the link below:
 https://www.tonymacx86.com/threads/an-idiots-guide-to-imessage.196827/

 Keep in mind that even if you have setup iMessage and FaceTime  correctly, newer AppleID(s) are not having much success as they do get  the message to call Apple Support.
 Contrary to this, old Apple ID(s) seems to be working perfect without having a single issue.
 If you do have a newer AppleID and you can't make iMessage and FaceTime  work, the only possible "current known" fix is to get an older Macbook  that is not being used anymore, dump the MLB and ROM.
 Generate your unique Serial Number and UUID as the guide describes and after you have correct setup:
 Just replace the generated MLB and ROM with the ones you got from the dump of the older Macbook.
 iMessage and FaceTime should now work correctly with your Unique Serial Number and UUID.

## **Customization**

**Themes**
 There is a huge list of available "Themes" across the web for Clover Bootloader which you can google.
 I included the ThinkPad theme which i also used previously on my  ThinkPad guides because i think it better fits these laptops, it is  included on the Lenovo-V330-15IKB folder Downloaded from my Github  Repository.
 To install it you simply copy the Thinkpad folder into EFI/Clover/Themes and set it as default theme on config.plist

### **System Logo**

For System Logo i use the laptop picture at the beginning of the guide  which i think is one of the best available and best quality one for use  as System Logo for this laptop.
 What i did is i created two versions: One with Light Mode Wallpaper and  One with Dark Mode Wallpaper as macOS Mojave has added the dynamic  System Logo option on "About this Mac"

 To use Dynamic System Logo you go to Applications > Utilites > System Information (right Click) > Show Contents.
 Go to Contents > Resources > Assets.car.
 Replace it with the Assets.car that included in the Lenovo-V330-15IKB folder downloaded from my Github repo.
 Examples with Light Mode and Dark Mode on the screenshots below

If you are use Catalina, please follow this. 

- Copy the Assets.car to a path

- Reboot into RecoveryOS and open a terminal to run:

  ```shell
  cd /Volumes/Catalina/System/Applications/Utilities/System\ Information.app/Contents/Resources
  cp /path/to/Assets.car ./
  ```

- Reboot and enjoy!

