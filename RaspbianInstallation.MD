1. Download Raspbian image:

https://www.raspberrypi.org/downloads/raspbian/

2. Connect Pi to PC

3. Find out device is your MicroSD:

sudo fdisk -l (should be something lime /dev/sdc)

4. Go to folder with Pi image to Unzip and flash the image:

unzip -p 2017-09-07-raspbian-stretch.zip | sudo dd bs=4M if=2017-09-07-raspbian-stretch.img of=/dev/sdc status=progress conv=fsync

5. Insert MicroSD to Pi and plug-in power.

Done!
