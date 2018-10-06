#### 1. Changing your root password:
* sudo passwd root

#### 2. Adding new user:
* sudo adduser -m vadim -G sudo
 
#### 3. Removing default user Pi:
* sudo su
* sudo deluser -f -remove-home pi
* sudo groupdel pi

#### 4. Make sudo require a password:
* **sudo nano /etc/sudoers.d/010_pi-nopasswd**
* and change the pi entry (or whatever usernames have superuser rights) to: **vadim ALL=(ALL) PASSWD: ALL**

#### 5. Enabling SSH login
* ssh-keygen -t rsa -b 4096
* cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
* chmod 644 ~/.ssh/authorized_keys
* **sudo nano /etc/ssh/sshd_config**:
  * uncomment **PubkeyAuthentication yes** 
  * uncomment and replace **#AuthorizedKeysFile** with **AuthorizedKeysFile      %h/.ssh/authorized_keys**
  * add **RSAAuthentication yes**
* sudo service ssh reload

#### 6. Disabling other authentification methods (apart from SSH pubkey):
* sudo nano /etc/ssh/sshd_config
* uncomment replace **#PasswordAuthentication** with **PasswordAuthentication no**
* check **ChallengeResponseAuthentication no** (should be "no")
* uncomment and replace **#UsePAM yes**with **UsePAM no**
* uncomment and set PermitRootLogin to **PermitRootLogin no**
* uncomment and set StrictModes to **StrictModes yes**
* uncomment **PermitEmptyPasswords no**
* sudo systemctl restart ssh

#### 7. Change default ssh port:
* sudo nano /etc/ssh/sshd_config
* change Port setting to **Port 777**
* sudo service ssh reload