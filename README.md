## openwrt for xiaomi Router 3G R3G v1  rom 128MB  ram 256MB

Installation via SSH for R3G v1
## This is not for R3G v2 

For installation via ssh, it needs to be enabled first. The following steps are based on this forum post and this post from Reddit.

Setup the router and install a [dev firmware], for example https:// cdn.cnbj1.fds.api.mi-img.com/xiaoqiang/rom/r3g/miwifi_r3g_firmware_12f97_2.25.124.bin

Install the Mi Wi-Fi app on a phone or tablet. (Android | there is also an iOS app)

Open the app and connect your router. Also sign in to link that router to your account. The router should be detected assuming you are connected to its WiFi and the router is connected to the internet. It might also work without that.

On a PC, visit https://d.miwifi.com/rom/ssh and sign-in to your account. It is important to have the https version. It might get switched to http and show an error. Changing that to https again should make the page load again. This is also the case for all clicks on that website, for example the download link will also probably only work if changing manually to https after getting an error. Alternatively, redirection and loading problems can be avoided by directly accessing the page. After signing-in to your xiaomi account get your “userID” (the number near your profile pic), then copy-paste it to the following link https://d.miwifi.com/rom/ssh?userId=<yourUserID>.
    
After login, a page with your router, root password for SSH access and a download button should be displayed. Press the download button to download the [ miwifi_ssh.bin ] file. If loading/redirection problems still persist, copy the download link (button on the right of the popup dialog) and visit it after adding “&userId=<yourUserID>”.
    
Format a USB drive with FAT32 and copy the downloaded miwifi_ssh.bin to it.
    
Shut down the router (unplug it) and put the USB drive in. Now you have to hold down the reset button of the router (use a paper-clip for example) while powering the router on (plugging the power cable in). Continue holding the button until you see the yellow LED start to flash. This might take a while ( 15 seconds). Now you can release the button. The router will reboot soon. Afterwards you should have SSH access.
    
Login to the router using SSH with root as username and the root password that is displayed on https://d.miwifi.com/rom/ssh.
    
Actual installation via SSH:

Copy ???????-kernel1.bin and ???????-rootfs0.bin ( optained from the releases ) to a USB drive   on the router
    
Switch to /extdisks/sda1/  
    
Run:
    
mtd write ???????-kernel1.bin kernel1
    
mtd write ???????-rootfs0.bin rootfs0
    
nvram set flag_try_sys1_failed=1
    
nvram commit
    
reboot



## 鸣谢 [![](https://img.shields.io/badge/-跪谢各大佬-FFFFFF.svg)](#鸣谢-)
 
[OpenWrt 官方库](https://github.com/openwrt/openwrt)

[P3TERX 的 Action 库](https://github.com/P3TERX/Actions-OpenWrt)

[Lean 的 OpenWrt 库](https://github.com/coolsnowwolf/lede)

[Lienol 的 Packages 库](https://github.com/Lienol/openwrt-packages)

[SuLingGG 的 OpenWrt-Rpi 库](https://github.com/SuLingGG/OpenWrt-Rpi)
