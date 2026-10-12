# RTL8812AU/14AU/21AU Wireless drivers
Only for use with Linux & Android.
This repository is a fork of [aircrack-ng/rtl8812au](https://github.com/aircrack-ng/rtl8812au). It supports kernel version 7.1.5 kali linux.

## Installation

### Download
```
$ sudo apt-get update
$ sudo apt-get install bc mokutil build-essential libelf-dev linux-headers-$(uname -r)
$ git clone https://github.com/Mrietes/rtl88XXau-kali-linux
cd rtl88XXau-kali-linux
```

### Method 1. DKMS
```
$ sudo apt-get install dkms
$ sudo make dkms_install
```
### Method 2. Make
For building & installing the driver with 'make' use
```
$ sudo make -j$(nproc) && sudo make install
```

### Removal of Driver
In order to remove the driver from your system open a terminal in the directory with the source code and execute the following command:
```
$ sudo make dkms_remove
```

### LED control
statically by module parameter in /etc/modprobe.d/8812au.conf or wherever, for example:
```
options 88XXau rtw_led_ctrl=0
```
value can be 0 or 1.
Or dynamically by writing to /proc/net/rtl8812au/$(your interface name)/led_ctrl, for example:
```
$ echo "0" > /proc/net/rtl8812au/$(your interface name)/led_ctrl
```
value can be 0 or 1.
Check current value:
```
$ cat /proc/net/rtl8812au/$(your interface name)/led_ctrl
```

### USB Mode Switch
```
$ rmmod 88XXau
$ modprobe 88XXau rtw_switch_usb_mode=int (0: no switch 1: switch from usb2 to usb3 2: switch from usb3 to usb2)
```

### NetworkManager

Newer versions of NetworkManager switches to random MAC address. Some users would prefer to use a fixed address.
Simply add these lines below.
```
[device]
wifi.scan-rand-mac-address=no
```
At the end of file /etc/NetworkManager/NetworkManager.conf and restart NetworkManager with the command:
```
$ sudo service NetworkManager restart
```
### Credits / Contributors

```
Alfa Networks - https://www.alfa.com.tw/
Realtek.      - https://www.realtek.com
aircrack-ng   - https://www.aircrack-ng.org

astsam        - https://github.com/astsam
evilphish     - https://github.com/evilphish
fariouche     - https://github.com/farioucheMethod 1.
CGarces       - https://github.com/CGarces
ZerBea        - https://github.com/ZerBea
lwfinger      - https://github.com/lwfinger
Ulli-Kroll.   - https://github.com/Ulli-Kroll

```
