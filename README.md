# Ubuntu-21.04.1-Hirsute-Hippo-pre-image-cho-Nexus-7-2012-wifi-rev.-E1565-kernel-5.14-rc3-next-grate
Linux on Nexus 7 2012

Ubuntu 21.04 Hirsute Hippo pre-image server armhf

https://drive.google.com/drive/folders/1jhq1v5ejOazDB1wSF-ZS0FxBc_QIPUFD



Cần có micro-usb keyboard để input trong command line



Cách kiểm tra Nexus 7 2012 là mã cũ PM269 hay E1565. Tham khao:

https://wiki.postmarketos.org/wiki/Google_Nexus_7_2012_(asus-grouper)



Variants

grouper rev. PM269 - without GSM (oldest)
grouper rev. E1565 - without GSM (modern revision)
tilapia rev. E1565 - with GSM



Do I have grouper or tilapia?



TWRP (adb shell) $ grep androidboot.baseband=unknown /proc/cmdline && echo grouper || echo tilapia



Which hardware revision of grouper do I have?





TWRP (adb shell) $ find /sys/devices/ | grep -c max776 && echo You have E1565



TWRP (adb shell) $ find /sys/devices/ | grep -c tps6591 && echo You have PM269



Đặt máy về bootloader, để flash boot.img qua fastboot hoặc dùng method của postmarketOS. Kết nối Nexus 7 vào máy tính qua cáp usb chuẩn 1.0 → 2.0



$ sudo adb start-server



$ sudo adb reboot bootloader



$ sudo fastboot flash boot <boot_filename>.img



Vào TWRP for grouper 3.3.1-0 trở lên https://dl.twrp.me/grouper/

Dùng adb shell trên PC/laptop hoặc Advance/Terminal trong twrp để umount mmcblk0p9 (làm 2 lần cho chắc ăn) [với tilapia (bản 3G) là mmcblk0p10]



1. TWRP(Advance → Terminal): $ df

2. TWRP(Advance → Terminal): $ umount /dev/block/mmcblk0p__  <- fill partition number

3. TWRP(Advance → Terminal): $ umount /dev/block/mmcblk0p__  <- fill partition number



On PC/Laptop terminal:



$ adb push <rootfs_filename>.img /dev/block/mmcblk0p__  <- fill partition number



grouper has likely data on /dev/block/mmcblk0p9 but make sure!
tilapia has likely data on /dev/block/mmcblk0p10 but make sure!



Khi cài bản ubuntu pre-image server này vào, ubuntu mặc định sẽ boot bằng cloud-init và vào thẳng root khi nhấn Enter

tại dòng thông báo



Bạn cần đổi passwd cho user ubuntu mặc định bằng



# sudo passwd ubuntu



# exit



login: ubuntu

passwd: [your_passwd]



Tạo wpa.conf cho kết nối wifi



# sudo su



# sudo wpa_passphrase [your_ssid_name] [your_router_passwd] > wpa.conf



Loading wpa.conf vào wpa_supplicant và ping thử google.com



# sudo wpa_supplicant -B -i wlan0 -c wpa.conf



# sudo dhclient wlan0



# sudo ping -c 3 google.com



# sudo apt update && sudo apt upgrade



# sudo add-apt-repository ppa:grate-driver/ppa



# sudo apt install alsa-ucm-conf libvdpau-tegra xserver-xorg-video-opentegra linux-firmware libd3dadapter9-mesa libegl-mesa0 libgbm1 libgl1-mesa-dri libglapi-mesa libglx-mesa0 libosmesa6 mesa-opencl-icd mesa-va-drivers mesa-vdpau-drivers mesa-vulkan-drivers



Cài DE như Lubuntu, Xubuntu, Kubuntu, MATE, GNOME, Phosh, Budgie, Cinamon, Elementary, v.v...



Trong /opt folder có các utils temp_throttle, cpufreq.start, clear_ram, sysctl.conf v.v…



Remove RaspBerryPi package

# sudo apt purge --auto-remove u-boot-rpi:armhf linux-firmware-raspi2 linux-headers-5.11.0-1007-raspi linux-headers-5.11.0-1016-raspi linux-headers-raspi linux-image-5.11.0-1007-raspi linux-image-5.11.0-1016-raspi linux-image-raspi linux-modules-5.11.0-1007-raspi linux-modules-5.11.0-1016-raspi linux-raspi linux-raspi-headers-5.11.0-1007 linux-raspi-headers-5.11.0-1016 ubuntu-raspi-settings



# sudo apt install bluez dconf-gsettings-backend dconf-services libdconf1



Remove cloud-init



# sudo dpkg-reconfigure cloud-init



# sudo systemctl stop cloud-init



# sudo systemctl disable cloud-init



# sudo apt purge --auto-remove cloud-init



# sudo rm -rf /etc/cloud/ && sudo rm -rf /var/lib/cloud/



# sudo systemctl daemon-reload



# sudo systemctl default



# sudo reboot



[MEDIA=youtube]qvZXIWfThgU[/MEDIA]
