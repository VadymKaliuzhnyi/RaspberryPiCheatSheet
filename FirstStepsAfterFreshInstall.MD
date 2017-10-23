<====== before u go into internet ======>

1. Change your root password:
sudo passwd root

2. Change your Pi (user) password:
sudo passwd pi

<====== u can go online now (but u r still not 100% safe) =====>

3. Connect to your Pi via ssh:
pi@192.168.1.20

4. Run Pi's config GUI:
sudo raspi-config

- to enable SSH
- set hostname
- disable "Start desktop on boot"
- set local timezone
- disable unsused interfaces
- overclock ^^

4. full system update:
yes | sudo apt-get update && yes | sudo apt-get upgrade && yes | sudo apt-get dist-upgrade | sudo reboot now

5. Set-up ssh keys for Laptop<=>Pi connection:
- On our laptop (not on Pi) check ssh keys direcroty:
ls ~/.ssh

- On lapotp create new Priv/Pub key pair:
ssh-keygen -t rsa -b 4096 -C PiKeys

- login to you Pi and create ssh dir there:
install -d -m 700 ~/.ssh

- from your laptop copy pub key to Pi:
cat ~/.ssh/id_rsa.pub | ssh pi@192.168.1.20 'cat >> .ssh/authorized_keys'

6. Remove user login (with password) and leave only ssh option

- go to ssh conf file:
sudo nano /etc/ssh/sshd_config

- turn off root login:
PermitRootLogin no

- turn off password login:
PasswordAuthentication no

<====== u are quite safe to surf online =====>

7. Install some musthave apps:
yes | sudo apt-get install iotop htop xrdp
