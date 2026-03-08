# attack-shark-r5-udev-rules
Udev rules for Attack Shark R5 Ultra mouse on Linux

in arch linux create new file in /etc/udev/rules.d/

name it 99-attackshark-mouse.rules

paste this inside



KERNEL=="hidraw*", ATTRS{idVendor}=="XXXX", ATTRS{idProduct}=="XXXX", MODE="0666", SYMLINK+="attackshark-r5-hidraw", TAG+="uaccess"
SUBSYSTEM=="usb", ATTRS{idVendor}=="XXXX", ATTRS{idProduct}=="XXXX", MODE="0666", TAG+="uaccess"

change XXXX to your mouse id by opening terminal and lsusb

first 4 numbers should go to ATTRS{idVendor}=="XXXX"
last 4 numbers should go to ATTRS{idProduct}=="XXXX"

do this on both top and bottom lines

save file

Reload: sudo udevadm control --reload-rules && sudo udevadm trigger


now the webdriver should work for you
