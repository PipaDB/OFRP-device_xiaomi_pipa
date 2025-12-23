# Orange Fox (OFRP) for Xiaomi Pad 6 (pipa)  
Built using Xiaomi Pad 6, HyperOS 1.0 (Android 13), compatible with OrangeFox Android 12 branch  

![OFRP](https://image.ibb.co/cTMWux/logo.jpg "OFRP")  
====================================================
# Current Status
- Display works normally  
- To ensure proper UI alignment, there are margins on the left and right sides of the screen  
- Basic recovery functions are working  
- If you encounter /data decryption failure after flashing HyperOS (Android 15), simply set a lock screen password after booting into the system  

# How to Use
Go to the [Release](https://github.com/pipaDB/OFRP-device_xiaomi_pipa/releases) page, expand the Assets section, and download the 7z archive.  
Extract all files, open the extracted folder, and run the `recovery-twrp一键刷入工具.bat` script to flash according to the prompts. If adb detects your device, it will automatically reboot into recovery.  
Thanks to wzsx150 for the flashing tool script.  

After a successful temporary boot, you can go to "Menu" > "More" > "Install current OrangeFox" > swipe to confirm, to install OrangeFox permanently to the boot partition, replacing the stock recovery.  
Alternatively, you can flash the OrangeFox zip installer to achieve the same.  
Permanently installing OrangeFox will replace the current ramdisk, so Magisk root will be lost.  
You need to flash the Magisk zip again to regain root,  
or backup your current boot image, patch it with Magisk, and restore it to have both OrangeFox and Magisk coexist.  
Apatch is not affected by permanent installation; installation order does not matter.  

Note:  
On VAB devices, after flashing a ROM, the next boot will switch to the other slot and requires a reboot to take effect.  
For example, if your current system is on slot a, the ROM will be flashed to slot b, and you need to reboot to boot into slot b.  
If you flash Magisk in recovery without rebooting, it will be installed to slot a, and slot b will not have root after booting.  

You can also use tools like "Gaiji Assistant" (PC version) or FastbootEnhance to simplify the flashing process.  

# How to Build
Download the OFRP source code and clone this device tree into the appropriate location.  
For example, if your OFRP source root is `~/fox_12.1`, place this repo at `~/fox_12.1/device/xiaomi/pipa/`:  
```bash
cd ~/fox_12.1
mkdir -p device/xiaomi
cd device/xiaomi
git clone https://github.com/pipaDB/OFRP-device_xiaomi_pipa.git pipa
```
From the source root directory, run:  
```bash
. build/envsetup.sh && lunch twrp_pipa-eng && mka bootimage
```

# Cloud Build
Use Github Actions to build OrangeFox online.  
For example, if your Github username is "JohnSmith":  
1. Open the [OrangeFox Action Builder](https://github.com/pipaDB/OrangeFox-Action-Builder) repo and click the `Fork` button in the top right corner.  
![image](https://user-images.githubusercontent.com/37921907/177914706-c92476c5-7e14-4fb3-be94-0c8a11dae874.png)
2. After the page redirects, you will see the new repo under your username.  
![image](https://user-images.githubusercontent.com/37921907/177915106-5bde6fc9-303c-479e-b290-22b48efd1e4e.png)
3. Go to the `Actions` tab > `All workflows` > `OrangeFox - Build` > `Run workflow`  
![image](https://user-images.githubusercontent.com/37921907/177915304-8731ed80-1d49-48c9-9848-70d0ac8f2720.png)
4. Fill in the parameters as follows:  
OrangeFox Branch  
`12.1`  
Custom Recovery Tree  
`https://github.com/ymdzq/OFRP-device_xiaomi_pipa`  
Custom Recovery Tree Branch  
`fox_12.1-a16`  
Specify your device path.  
`device/xiaomi/pipa`  
Specify your Device Codename.  
`pipa`  
Specify your Build Target  
`boot`  
![image](https://user-images.githubusercontent.com/37921907/177915346-71c29149-78fb-4a00-996f-5d84ffc9eb8c.png)
5. After filling in, click "Run workflow" to start the build.
6. You can download the build result from the Releases page of your forked repo.
