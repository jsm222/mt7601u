# mt7601u
Also see https://bugs.freebsd.org/bugzilla/show_bug.cgi?id=247545
**Expect crashes** Mostly tested on 
FreeBSD 14.0-ALPHA1 amd64 1400094 #0 main-n264678-136fc495615f: Fri Aug 11 08:18:04 UTC 2023     root@releng1.nyi.freebsd.org:/usr/obj/usr/src/amd64.amd64/sys/GENERIC amd64

Makefilefw1  is for revisions not supported for now.
Works with open networks. ~~Not tested with WPA~~  /WEP ~~WPA2~~ yet. Only tested as station. 
Only hardware version 
**7601** is covered now (there is also a 7612 and 7610 not working) 
I did not include the code for the others yet (I do not own the specific hardware).

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

**if that fails on 13.2** try to use rc.conf and loader.conf instead (not tested)

~~Nothing works as of now in this repo. I have some not committed progress, where the firmware loads and it can scan, and associate to open networks~~
