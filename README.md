# OpenCore-Steam-Deck
![image](https://github.com/user-attachments/assets/7d3877d3-b9c4-4c05-a999-4d8caf38b596)


An OpenCore EFI configuration for the Steam Deck

This is a guide targeted at getting users to run macOS bare metal on their Steam Decks.

Some things to know:

1. Not everything works. Many devices do not have support. This is more of a "Look what I can do!" thing as of right now.

2. THIS CAN EASILY WIPE YOUR STEAMOS INSTALL IF YOU ARE NOT CAREFUL. Part of the macOS install is FORMATTING a storage device OF YOUR CHOOSING. IF YOU CHOOSE THE INTERNAL STORAGE OF THE STEAM DECK, IT WILL BE WIPED.

3. With #2 being said, you can, in fact, dual boot macOS and steamOS or windows on the same drive with some elbow grease.

4. I did not make any of the software used. I simply helped get macOS booting with some other devs and people interested. It was a team effort.

5. Stuff will be fixed or not depending on if someone takes interest and adds support. PLEASE dont ask when stuff with be supported, I dont know.

6. PLEASE DO NOT FLOOD THE HACKINTOSH SERVERS FOR SUPPORT REQUESTS. Whether it be discord or others. These are niche devices that barely run macOS. For the love of all thats good and holy, dont pester the volunteers that help others with this meme of a computer. If you must ask, come here to and ask IN THE DISCUSSIONS.


**Getting Started**

Firstly, you need to understand how to run macOS on any other PC. Go to the [Dortania OpenCore install guide](https://dortania.github.io/OpenCore-Install-Guide/) and familiarize yourself with it. This is what we will be using.

For the most part, you will follow the steps in the OpenCore guide, so make sure that you read and understand it.

As you are following the guide and get to the [Gathering Files](https://dortania.github.io/OpenCore-Install-Guide/ktext.html) portion, you will want to have these files for the Steam Deck:


**APCI**

For this, you are going to want to download a tool called [SSDTTime](https://github.com/corpnewt/SSDTTime). Running this tool, you are first going to choose option **P** to dump you DSDT. Then you are going to select option **3** to make a SSDT-EC.aml. It should be in the resaults folder. Copy this to your EFI -> APCI folder, as per the OpenCore guide instructions.

You will also need the [SSDT-CPUR](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-CPUR.aml) in the ACPI folder.

In the end, you should have two files in the ACPI  folder:

1. SSDT-CPUR.aml
2. SSDT-EC.aml
   

**Firmware Drivers**

You only need two firmware drivers:

1. [HfsPlus.efi](https://github.com/acidanthera/OcBinaryData/blob/master/Drivers/HfsPlus.efi)
2. OpenRuntime.efi (included in the OpenCore drivers folder already)

Everything other than these two .efi files be trashed. In fact, I recommend that you trash all the extras (there are alot) so the boot menu for OpenCore isnt a confusing mess.


**Tools and Resources**

Just drag the tools and the resources folders to the trash. Yes im serious, we dont need them right now, just get rid of them.


**Kexts**

*Note: Kexts with look like regular folders with .kext at the end on Windows and Linux. Just get the folders with the .kext at the end, these are what you want*

Make sure you have these Kexts in your kexts folder:

1. [Lilu.kext](https://github.com/acidanthera/Lilu/releases)
2. [VirtualSMC.kext](https://github.com/acidanthera/VirtualSMC/releases) *Only the VirtualSMC.kext is needed, none of the others in the folder*
3. [GUX-RyzenXHCIFix](https://github.com/RattletraPM/GUX-RyzenXHCIFix/releases/tag/v1.3.0b1-ryzenxhcifix) *This kext is experimental! Make sure you read its readme!*
4. [USBToolBox.kext](https://github.com/USBToolBox/kext/releases)
5. For USBMap.kext, you can make your own with the [tool](https://github.com/USBToolBox/tool) with REQUIRES Windows and DOES NOT support Linux, or if you dont have Windows, you can use [this](https://github.com/CodeRunner5235/Opencore-Steam-Deck/blob/main/UTBMap.zip) map which *should* work, but dont be surprised if it stops working

6. [AppleMCEReporterDisabler.kext](https://github.com/acidanthera/bugtracker/files/3703498/AppleMCEReporterDisabler.kext.zip) is only needed for macOS versions newer than *but not including* Big Sur.
   

**Config.plist**

After nabbing the sample.plist from the OpenCorepkg -> docs folder, moving it to your OC folder and renaming it config.plist, follow the steps in that [Ryzen and Threadripper portion of the guide](https://dortania.github.io/OpenCore-Install-Guide/AMD/zen.html) with just a few variations:

1. You can leave Booter -> Quirks -> ResizeAppleGpuBars as -1 for now.

2. For your AMD patches under the Kernel, the Steam Deck uses **4 cores** and 8 threads, so you will want to use 4 in your AMD patches.

3. Under Kernel -> Quirks, we have a USB map so make sure to **disable** the XhciPortLimit

4. Under Misc -> Security, set SecureBootModel to Disabled to make life easier.

5. Under your NVRAM section in your boot-args, add vsmcgen=1 at the end.

6. For PlatformInfo, something like MacBookPro16,3 works fine.

7. Under UEFI -> Output, set DirectGopRendering to True and set the Resolution to 1280x720
   *Note: If you skip this last part, your screen output will be garbled*



That should do it! Just these changes the the standard OpenCore Ryzen install guide should get you up and running. Have fun!


**Picture Examples**

*OC folder*
![image](https://github.com/user-attachments/assets/4f42c205-2a4a-4b3b-b24f-3e16e08a5e07)


*ACPI folder*
![image](https://github.com/user-attachments/assets/bf2fbe09-fbb3-43ce-b97d-cdc7109b469a)


*Drivers folder*
![image](https://github.com/user-attachments/assets/52ffe87a-b5cb-4a3c-8ca1-ba5b1d309aa1)


*Kexts folder*
![image](https://github.com/user-attachments/assets/b0fc4d40-4adf-4b85-aff5-96067341c09a)





