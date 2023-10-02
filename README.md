# AsusB450M-II_Ryzen5600X_Hackintosh

***\*Hackintosh EFI Information for Asus B450M-II with Ryzen 5600X - Fully working, OC90, MacOS13.4\****

*MAJOR CHANGES: *

First Release - no major changes.  BIOS 4002 (2023/03/21) is used.  

Second Release - No EFI changes whatsoever (use OCAT to update; see guide here:  https://github.com/dclive/Howto--Update-OpenCore-with-OCAT); the only updates at this time (1-October-2023) are due to BIOS 4204 dated Sept 4 2023, found here:  https://www.asus.com/us/motherboards-components/motherboards/prime/prime-b450m-a-ii/helpdesk_bios/?model2Name=PRIME-B450M-A-II).  I suggest updating to this BIOS, and enabling PBO for a mild performance boost, shown below in the GeekBench section.

Sonoma MacOS 14 Statement:  This EFI / Setup seems to crash when I try to install Sonoma.  No further update at this time.

![229230925-1fc9cda2-0da5-46b3-ac8e-f40596f496f1.png (281×526)](https://user-images.githubusercontent.com/4536776/229230925-1fc9cda2-0da5-46b3-ac8e-f40596f496f1.png)

**Typical is Geekbench 6.x scores of 1931 single and 8182 multi-core, using PC3000 RAM, and 3.5% higher MC with faster RAM.  

PC3000 RAM:

![img](https://user-images.githubusercontent.com/4536776/229231646-e6ccb3e0-7b5c-415f-8694-3262d7e9e9e2.png)

PC3600 RAM: 

![233856753-5652edd7-5bc1-470c-9019-c617b7c6c3e2](https://user-images.githubusercontent.com/4536776/233856753-5652edd7-5bc1-470c-9019-c617b7c6c3e2.jpg)

Same PC3600 RAM, but with 4204 Sept 4 2023 BIOS and PBO enabled: 

![image](https://user-images.githubusercontent.com/4536776/271873967-53e24c32-e475-452e-88e0-4418e9ca315a.png)

**Credits**

Most content was sourced from a variety of internet sources, coupled with the Dortania guide, plus https://dortania.github.io/OpenCore-Install-Guide/AMD/zen.html#cleaning-up the AMD bits, and https://github.com/AMD-OSX/AMD_Vanilla for more AMD bits.  Note that the best AMD kernel patch I found was Shanee's, not Algrey's (see that second link...) - Algrey's gave me horrible GPU performance; Shanee's improved things, but at the cost of spotty audio (I survive...), whether over USB, DP, HDMI, or whathaveyou.  

If you must have perfect audio, Intel may be a better choice.  

**Tested macOS**

- OC90+ and Ventura 13.6+ is the only focus of current testing.

**Hardware**

- Asus Prime B450M-II  works well in MacOS Ventura 13.6. It's safe to update, and all testing will only include 4204 BIOS (or later) going forward. Flash to 4024 (see above). After Flash, load all BIOS defaults. Then disable GPU ReBar, disable serial, disable secure boot, disable fast boot, disable CSM.  Set XMP to on (if your RAM is capable).  Enable above 4G Decoding.  
- Ryzen 5600X [If you use another Ryzen chip with a different number of cores, changes are required]
- An AMD GPU is required regardless of which Ryzen CPU you use, no exceptions; ADGPMOD=PIKERA is in place for allowing any of the newer supported GPUs without issue.  The AMD580 and AMD5700 are directly tested.
  - Most typical, RX470, RX480, RX570, RX580, RX590, Vega 56, Vega 64, RX 5700, RX6600, RX6600XT, RX6800, RX6800XT, RX6900XT will all work. Some other variants (some RX560, for example) will work also, but you should google for more details before buying. 
- 64GB RAM PC3600 [2 x 32GB DIMMs]
- 1TB NVME [HP EX920]
- Generic EVGA 550W PSU
- Phanteks Enthoo Evolv MATX Tempered Glass Case.
- I do not use wifi or bluetooth on this machine in any capacity; you're on your own.  I strongly suggest Broadcom/Fenvi.  You'll need to map that port, depending on where you plug in the wireless/BT adapter.  Note with Sonoma you'll probably want to flip to Intel BT/Wifi.  Haven't tried with this motherboard / cannot provide support.

**Working**

- AMD GPU; AMD GPU audio via HDMI/DP, or aftermarket USB works, but has issues.
- Sleep / Wake works; mouse / keyboard wakes machine; no motherboard 'internal' USB2 headers are enabled; the internal USB3 header is used, only.  I find I must press the power button on my case, and then the Mac immediately wakes (in about 1 second)
- App Store, Time Machine [But to recover, keep track of your USB stick with your serials/MAC Address/etc. embedded in it!]
- USB port mapping is complete and believed to work fine.

**Untested**

- 3.5MM audio is untested.

**Not Working**

- Anything using wifi / BT won't work (unless you add the hardware and the USB mapping); anything based on Intel QuickSync won't work.  I find emulation, like Fusion, won't work, nor will common photo apps, like Topaz Photo AI and Topaz Video AI; they simply quit.  I suspect it's due to the AMD Ryzen CPU, as these apps run fine on my Intel CPU Hacks.  

**Next Steps - Required**

You will need to do the following:

- Prepare a USB boot disk for MacOS 13.x installation. The easiest way is on a real Mac, although gibMacOS may work for you as well. To follow the much easier Real Mac path, read https://support.apple.com/en-us/HT201372 and follow the directions for MacOS, including the terminal command to write the download to the USB stick. You'll want to format the USB as HFS+ format, GUID. TINU also can make a bootable USB stick...
- Download EFIAgent (https://github.com/headkaze/EFI-Agent) and mount the EFI (ESP) partition for the USB stick you just made. Using EFIAgent again, "open" the EFI partition so it shows on the Mac desktop. Note that EFI partitions are typically GRAY in color in EFIAgent. To find EFIAgent, locate the new icon in the upper right clock area that looks like a circular pie. [![Screen Shot 2021-09-25 at 7 22 44 PM](https://user-images.githubusercontent.com/4536776/134790066-27597b9e-a37f-47e0-87f5-d3ebbc2af59f.png)](https://user-images.githubusercontent.com/4536776/134790066-27597b9e-a37f-47e0-87f5-d3ebbc2af59f.png)

> > Remember this process for any future EFI partitions you must mount; this is a common procedure.

- Copy the contents of the attached zipfile to the USB stick, so that your files look something like the picture:

[![EFI Layout](https://user-images.githubusercontent.com/4536776/134783624-10b0c7ba-fb29-4cf1-8017-230d22f8e18b.png)](https://user-images.githubusercontent.com/4536776/134783624-10b0c7ba-fb29-4cf1-8017-230d22f8e18b.png)

- The EFI (ESP) partition on the USB stick has an EFI folder in it, in the root, and inside of that folder, there are two subfolders, OC and Boot, each with files in them. Make sure your EFI partition looks just like this once you've unzipped the zipfile.
- Note that you'll have TWO partitions on that one USB stick: the EFS/EFI partition (which has just the EFI folder on it, with the contents above) and the other partition, usually called 'Install MacOS Ventura' which will house the Mac's OS/installation details.

Technically, you are now done. You should be able to boot MacOS using the USB stick, and install MacOS onto your SSD. That said, I usually suggest configuring it a bit *after* you boot into MacOS for the first time with the right serials and ROM info:

- Download OCAT https://github.com/ic005k/QtOpenCoreConfig and open it. Read the tooltips showing what all the icons at the top do. Update to the latest OCAT version by finding the update button and updating. Don't continue until you've done this. Run the latest OCAT version. As of last edit, OC90 is current and fully working. Over the course of time further updates will be required. Become familiar with how to pull the latest OCxx release and KEXT updates from within OCAT 'into' your EFI configuration; you will do this a lot.
- Open your USB stick's config.plist by using OCAT's OPEN icon.
- In OCAT, notice the row of icons on the left side. Go to "PI" on the row.
- Let's generate a new serial. Ensure, under the GENERIC tab, that for "SystemProductName" you have the iMacPro1,1. Then click GENERATE right next to the iMacPro1,1 box. Your serial numbers are now set up.
- Note you can also use the GenSMBIOS command to do all this too (https://github.com/corpnewt/GenSMBIOS)

Now let's fix your MAC address (ROM)

- [Mac: This only works if you used the USB stick to install MacOS already; assumes MacOS is installed on this motherboard] Go to the Mac's terminal, type in "ifconfig", and find "en0:", your ethernet adapter. Find the line "ether xx:xx:xx:xx:xx:xx" and write those numbers, without the :, into the ROM box.
- [Using Windows, if Windows is installed on this motherboard] Go to Windows' commandline/powershell interface. Type 'ipconfig /all' and find your ethernet adapter. Find the line "Physical Address" with xx-xx-xx-xx-xx-xx letters to the right on that same line. Key in those letters and numbers, without the -, in the ROM box.
- [The easy way; untested] Click GENERATE immediately to the right of the ROM box.
- Serialization and ROM setup is now complete. Press the SAVE icon in OCAT and then quit OCAT.
- Your USB stick is ready to use to boot your Mac and install MacOS.
- **After all of the above: Go to Dortania's page and read - before logging in with any AppleID accounts. https://dortania.github.io/OpenCore-Post-Install/universal/iservices.html**

**Final Steps**

- Assuming no other issues, your setup is now complete!
- Restart, press DEL at the Asus boot screen, go into BIOS, choose a boot disk, and boot from the USB stick (select the uEFI option if prompted). You'll then be able to step through installation of MacOS. You'll need to format your SSD as APFS or HFS+ (APFS is the new one; use that). Name the newly formatted SSD something like **MacSSD** so you know that's what you'll boot from in the future. Then you can start setup.
- Once setup is done, use EFIAgent or OCAT to copy the USB stick's EFI folder, with your serial number modifications, to the SSD's EPS (EFI) partition, and then you'll be able to boot from that disk (and you won't need the USB stick anymore, but keep it forever as a backup!). Do note: Until you've copied the EFI folder from your USB stick to your SSD's EPS (EFI) partition, you must continue to use DEL to boot into your USB stick before booting into MacOS. Once you've copied the USB stick's EFI folder to the EPS (EFI) partition on the SSD, then you'll no longer need to use the USB stick to boot, and you'll just boot from the SSD's EPS (EFI).
- Versioning on this zipfile is OC90. Future versions, if required, would have higher numbers so it is easier to see what version you have. Keep the zipfile (name, at least) around so you know what version you have.
- You can clean up logs and logging / bootup, if you wish, once you have everything sorted. Doritania's guide has a post-install cleanup section with good details on that. In the zip, logging is fully enabled, so that if there's a problem you can take a video of the screen on your phone and troubleshoot based on that.
- **Use OCAuxiliaryTools to update to later OpenCore releases**. Use MacOS's built-in update mechanism to update MacOS releases.
- Otherwise, please leave comments/issues here.

**Benchmark Expectations**

- Running 13.6 with BIOS 4204 and a Ryzen 5600X, and using PC3600 RAM, I get GeekBench 6.2 scores of 1958/9278 (single/multi-core).
- A typical M2 base $499 mini (https://browser.geekbench.com/macs/mac-mini-2023-8c-cpu) is (Geekbench) 2629/9733, so the base 5600X is about 74% of the M2's speed per core, and about 95% of the M2 (mini) speed with all cores working.

**Addendum: OC90+**

- Use OCAT to update. No issues to report. DO THIS. It's worth staying current and fully fixed.  OC92 as of 5/2023 is fully working, and takes moments to update via OCAT.  See my OCAT procedure for full details.  https://github.com/dclive/Howto--Update-OpenCore-with-OCAT
