# mt7601u
To build add product ```RALINK MT7601		0x7601	Mediatek  Wireless Adapter```
to  ```/usr/src/sys/dev/usbdevs``` below the other RALINK products e.g
```
product RALINK RT2573_2		0x9021	RT2501USB Wireless Adapter
```
if needed do a make clean to update those changes

The module is not autoloaded so kldload /boot/modules/if_mtw.ko before you start the interface,
if it detaches because of waiting for MCU initializing then try to unplug and reinsert the device.

Also see https://bugs.freebsd.org/bugzilla/show_bug.cgi?id=247545

**Expect crashes** Mostly tested on 
FreeBSD 14.0-ALPHA1 amd64 1400094 #0 main-n264678-136fc495615f: Fri Aug 11 08:18:04 UTC 2023     root@releng1.nyi.freebsd.org:/usr/obj/usr/src/amd64.amd64/sys/GENERIC amd64
and FreeBSD 13.2-RELEASE releng/13.2-n254617-525ecfdad597 GENERIC amd64
Makefilefw1  is for revisions not supported for now.
Works with open networks. ~~Not tested with WPA~~  /WEP ~~WPA2~~ yet. Only tested as station. 
Only hardware version 
**7601** is covered now (there is also a 7612 and 7610 not working) 
I did not include the code for the others yet (I do not own the specific hardware).

**Since the OpenBSD driver this is based on does not support WME or 11n both are not possible at the momemnt.***

TO build fw goto fwdirectory
```
make -f Makefilefw
make -f Makefilefw install
```
to load fw 
```
kldload /boot/modules/mt7601u 
```
To build and load the module
```
make
make install
kldload /boot/modules/if_mtw.ko
```

then 

``` 
ifconifg wlan0 create wlandev mtw0 country <YOUR regdomain country>
make wpa_supplicant.conf with key_mgmt=NONE and ssid your ssid
```
then assuming dhcp dhclient wlan0

**if that fails on 13.2** try to use rc.conf

```
wlans_mtw0="wlan0"
ifconfig_wlan0="WPA SYNCDHCP"
```

~~Nothing works as of now in this repo. I have some not committed progress, where the firmware loads and it can scan, and associate to open networks~~
