Attack Shark R5 Mouse Webdriver Udev Setup Guide for Arch Linux and CachyOS

## Introduction
This guide provides a comprehensive setup for the Attack Shark R5 mouse webdriver using udev on Arch Linux and CachyOS, covering device ID discovery, rule creation, troubleshooting, and verification.

## 1. Discovering Device ID
To identify the device ID of your Attack Shark R5 mouse, use the following command:
```bash
lsusb
```
Look for an entry corresponding to the Attack Shark R5 mouse. The output will show the Vendor ID and Product ID, which will look similar to this:
```
Bus 001 Device 005: ID 1234:abcd Attack Shark R5
```
Note down `1234` as the Vendor ID and `abcd` as the Product ID.

## 2. Creating Udev Rule
To create a udev rule for the Attack Shark R5 mouse, follow these steps:
1. Open a terminal and create a new udev rule file:
   ```bash
   sudo nano /etc/udev/rules.d/99-attackshark.rules
   ```
2. Add the following line to the file, replacing `<vendor_id>` and `<product_id>` with the values you noted:
   ```
   SUBSYSTEM=="input", ATTR{idVendor}=="<vendor_id>", ATTR{idProduct}=="<product_id>", MODE="0666"
   ```
   Example:
   ```
   SUBSYSTEM=="input", ATTR{idVendor}=="1234", ATTR{idProduct}=="abcd", MODE="0666"
   ```
3. Save and exit the text editor (in nano, press `CTRL + X`, then `Y`, and `Enter`).

## 3. Reloading Udev Rules
To activate the new rules, reload the udev rules with the following command:
```bash
sudo udevadm control --reload-rules
sudo udevadm trigger
```

## 4. Troubleshooting
- **Mouse not detected:** Ensure that the Vendor ID and Product ID are correct, and that your user has permission to access the device. Check the output of `dmesg` for errors.
- **Permissions issues:** If regular users cannot access the mouse, make sure the udev rule sets the correct permissions.

## 5. Verification
To verify that the udev rule is working, plug in your Attack Shark R5 mouse and run:
```bash
devices
```
You should see your mouse listed with the correct permissions. If it’s not recognized, check your udev rule and troubleshoot as necessary.
