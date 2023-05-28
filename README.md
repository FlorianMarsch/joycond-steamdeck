# joycond-steamdeck
A patch for Joycond for the Steamdeck.

## Reason
While installing Joycond on my steamdeck i notice that my Conroller was not funcioning anymore. I conneced it thru Bluetooth and noticed that the joycond-cemuhook was not finding any input device. Also i figured that the controller was not working at all...

After some research i found that other had the same Problem (https://github.com/DanielOgorchock/joycond/issues/84). Unfortuently the provided solution was not accepted. This repository will contain patches needed to make our controllers work on Steamdeck. Please use on your own risk. Also please be aware that the described problem might not occur in case of a wired connection.

## Tested
[x] GULIkit KingKong 2 Pro Wireless Controller in Switch-mode

## Prerequirements

There are a few but baiscally install Joycond first! (source https://github.com/DanielOgorchock/joycond/issues/102)

```sh
sudo steamos-readonly disable
sudo pacman-key --init
sudo pacman-key --populate archlinux
#This may not be necessary:
sudo pacman -S bc
#Added --overwrite because fakeroot file already exists:
sudo pacman -S --overwrite \* base-devel
sudo pacman -S linux-neptune-headers
sudo pacman -S glibc linux-api-headers
sudo pacman -Qknq | cut -d' ' -f 1 | sudo pacman -S -

yay -Sy hid-nintendo-dkms
#Needed for single Joycons to show up in steam:
yay -Sy nintendo-udev
yay -Sy joycond-git
#Needed for joycon gyro support in UDP input applications:
yay -Sy joycond-cemuhook-git
sudo modprobe hid-nintendo
sudo systemctl enable --now joycond
```

## Install
```sh
git clone https://github.com/FlorianMarsch/joycond-steamdeck.git
cd joycond-steamdeck
cp ./udev/rules.d/89-joycond.rules  usr/lib/udev/rules.d/89-joycond.rules
sudo udevadm control --reload-rules && sudo udevadm trigger
```