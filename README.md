## 写在前面

小米R3G 路由器v1版 算是一个不错的路由器。 （不是v2版） 
CPU是MT7621 相当于两个MT7620 ， rom是128MB  ram是256MB， 足够安装一堆插件， 包括transmission下载  广告屏蔽 ， zerotier 等等插件都有。 
支持usb的优盘用transmission下载。 
5G信号是单频 但也够用， 使用802.11s和802.11kvr可以组mesh。  
支持ipv6-PD下发ipv6，所以没必要改光猫的拨号， 直接用光猫拨号就可以，把r3g的wan口接dhcp就行，r3g的lan设备都可以得到ipv6地址。  
性能方面，用5G测速到500Mbps没问题。 如果是fast.com 那么使用vless协议可以达到40Mbps 也足够应付16Mbps的4K视频。  MT7621的性能限制，不支持硬解码AES，所以这块比较吃亏。 zerotier因为只有单线程使用cpu，所以速度只能达到10Mbps。但是总体来说可以满足日常所需。 

路由器除了性能，最主要就是要求稳定。 所以本仓库提供稳定版在release 2022.02.16-1839， 通过breed或者openwrt升级刷入openwrt-ramips-mt7621-xiaomi_mi-router-3g-squashfs-sysupgrade.bin 就可以了。 如果是初次刷入，可以按照以下说明 刷入 openwrt-ramips-mt7621-xiaomi_mi-router-3g-squashfs-kernel1.bin 和 openwrt-ramips-mt7621-xiaomi_mi-router-3g-squashfs-rootfs0.bin。  

因为lede的openwrt每天都在更新，但是对于r3g这种老设备来说意义不大，硬件驱动如果能稳定工作其实就没必要修改，我试着更新编译新版的lede，但是经常编译失败，或者编译成功的也各种毛病。 所以就不再编译了，用2月16日的版本就挺好，该有的功能都有了，开机一个月都不会死机。 就算更新，也只更新插件的ipk就行了。 插件只能更新xray和zerotier这种插件的ipk，其他的内核级包括firewall iptables这种插件万万不能更新，一更新就死。

记住只要程序能跑，就不要更新。


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
