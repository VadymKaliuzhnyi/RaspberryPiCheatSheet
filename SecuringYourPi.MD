#### 1. Changing your root password:
* Login thru ssh as default pi user (login: **pi**, default password: **raspberry**)
* **sudo passwd root**

#### 2. Adding new user:
* **sudo adduser vadim && \\\
sudo usermod -aG sudo vadim**
 
#### 3. Removing default user Pi:

* Login thru ssh as new user (vadim)
* **sudo deluser -f -remove-home pi && \\\
sudo groupdel pi**
* check **cut -d: -f1 /etc/passwd | grep pi**

#### 4. Make sudo require a password:
* **sudo nano /etc/sudoers.d/010_pi-nopasswd**
* and change the pi entry (or whatever usernames have superuser rights) to: **vadim ALL=(ALL) PASSWD: ALL**

#### 5. Enabling SSH login
5.1 Generate new SSH keys:
* [in PC cli] **ssh-keygen -t rsa -b 4096** (and follow-up wizard)
* [in PC cli] **ssh-copy-id vadim@192.168.1.15**

5.2 Utilizing existing keys (optional if you skipped 5.1):
* [in Pi cli] **sudo mkdir ~/.ssh** (preparing dir for keys)
* [in PC cli] **scp ~/.ssh/\*.pub vadim@192.168.1.15:~/.ssh/**
* [in Pi cli] **cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys**

5.3 Configuring SSH service:
* **sudo nano /etc/ssh/sshd_config**
  * uncomment **PubkeyAuthentication yes** 
  * uncomment and replace **#AuthorizedKeysFile** with **AuthorizedKeysFile      /home/vadim/.ssh/authorized_keys**
  * add **RSAAuthentication yes**
* **sudo service ssh reload**

#### 6. Disabling other authentification methods (apart from SSH pubkey):
* **chmod g-w /home/vadim**
* **chmod 700 /home/vadim/.ssh**
* **chmod 600 /home/vadim/.ssh/authorized_keys**

* [in Pi cli] **sudo tail -f /var/log/auth.log | grep 'sshd'**
* [in PC cli] Check if this works **ssh -vvv -o PreferredAuthentications=publickey vadim@192.168.1.15**

* **sudo nano /etc/ssh/sshd_config**
* uncomment replace **#PasswordAuthentication** with **PasswordAuthentication no**
* check **ChallengeResponseAuthentication no** (should be "no")
* uncomment and replace **#UsePAM yes** with **UsePAM no**
* uncomment and set **PermitRootLogin** to **PermitRootLogin no**
* uncomment and set **StrictModes** to **StrictModes yes**
* uncomment **PermitEmptyPasswords no**
* **sudo systemctl restart ssh**

#### 7. Change default ssh port:
* sudo nano /etc/ssh/sshd_config
* change Port setting to **Port 777**
* sudo service ssh reload
