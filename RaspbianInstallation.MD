#### 1. Connect MicroSD card to PC (thru microSD USB reader or CardReader)

#### 2. Download Raspbian image:
[https://www.raspberrypi.org/downloads/raspbian/](https://www.raspberrypi.org/downloads/raspbian/)

My recommendation **Raspbian Stretch Lite**

#### 3. Flashing ISO to MicroSD:
3.1 LINUX - console way:
* Find out device is your MicroSD: sudo fdisk -l (should be something lime /dev/sdc)

* Go to folder with Pi image to unzip and flash the image, open terminal and run: 

  unzip -p **2018-11-13-raspbian-stretch-lite.zip** | sudo dd bs=4M if=**2018-11-13-raspbian-stretch-lite.zip** of=**/dev/sdc** status=progress conv=fsync
  
3.2 Linux - UI way:

* Download Etcher: [https://www.balena.io/etcher/](https://www.balena.io/etcher/)

* In Etcher - flash downloaded ISO to MicroSD card 

3.2 Windows:

* Donwload MicroSD card formatter:
[https://www.sdcard.org/downloads/formatter_4/index.html](https://www.sdcard.org/downloads/formatter_4/index.html)

* Format MicroSD Card via card formatter

* Download Etcher:
[https://www.balena.io/etcher/](https://www.balena.io/etcher/)

* In Etcher - flash downloaded ISO to MicroSD card 

#### 4. Insert MicroSD to Pi and plug-in power.

#### 5. Login for first time

If you've downloaded **Raspbian Stretch Lite** you will jump right into cli.

Default username: **pi**

Default password: **raspberry**

#### 6. After GUI will start in raspberry GUI configuration tool:

Run **sudo raspi-config**

* enable SSH interface
* enable overclock
* set language and timezone
* disable GUI login, enable CLI-way login, enable autologin to cli

#### 7. Update your PI:

After reboot in Pi terminal or thru SSH (login: **pi**, default password: **raspberry**):

**sudo apt-get update && \\\
sudo apt-get upgrade -y && \\\
sudo apt-get dist-upgrade -y && \\\
sudo apt-get update && \\\
sudo apt-get autoclean && \\\
sudo apt-get clean && \\\
sudo apt-get autoremove && \\\
sudo reboot now**
