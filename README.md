# xiaomi13pro
```bash
#!/bin/bash

# install package build dependencies
sudo pacman -S --needed base-devel git

# clone the nbfc AUR repo
git clone https://aur.archlinux.org/nbfc-git.git

# change directory to nbfc-git
cd nbfc-git

# build and install the package
makepkg -si

# change directory back
cd ..

# remove the cloned directory
rm -rf nbfc-git

# install intel-undervolt
sudo pacman -S intel-undervolt

# set up NBFC for the 'Xiaomi Mi Book (TM1613, TM1703)' profile
sudo nbfc config -a 'Xiaomi Mi Book (TM1613, TM1703)'
sudo nbfc start

# undervolt settings
# adjust these values based on your hardware and testing
sudo sed -i 's/undervolt 0 .*/undervolt 0 'CPU' -100/' /etc/intel-undervolt.conf
sudo sed -i 's/undervolt 1 .*/undervolt 1 'GPU' -50/' /etc/intel-undervolt.conf
sudo sed -i 's/undervolt 2 .*/undervolt 2 'CPU Cache' -100/' /etc/intel-undervolt.conf
sudo sed -i 's/undervolt 3 .*/undervolt 3 'System Agent' -50/' /etc/intel-undervolt.conf
sudo sed -i 's/undervolt 4 .*/undervolt 4 'Analog I/O' -50/' /etc/intel-undervolt.conf

# enable undervolting
sudo sed -i 's/enable .*/enable 1/' /etc/intel-undervolt.conf

# apply the undervolt
sudo intel-undervolt apply

# enable the systemd service
sudo systemctl enable --now intel-undervolt

# reminder to add BUSID to Bumblebee
echo "Please ensure to add the correct BUSID to your Bumblebee configuration in /etc/bumblebee/xorg.conf.nvidia"
```
