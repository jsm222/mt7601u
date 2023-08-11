# mt7601u
Also see https://bugs.freebsd.org/bugzilla/show_bug.cgi?id=247545
**Expect crashes** 
Makefilefw1  is for revisions not supported for now.
Works with open networks. Not tested with WPA/WEP WPA2 and so on yet. Only tested as stattion. 
Only version 
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
