# wpa\_supplicant

There's a service named `wpa_supplicant` configured by `/etc/wpa_supplicant/wpa_supplicant.conf`, `wpa_passphrase` can be used to create a config with hashed password (to put into the config file)

## wpa\_cli

Command line interface for `wpa_supplicant`

```
$ sudo wpa_cli 
wpa_cli v2.10
Copyright (c) 2004-2022, Jouni Malinen <j@w1.fi> and contributors

This software may be distributed under the terms of the BSD license.
See README for more details.


Selected interface 'wlp0s20f3'

Interactive mode

> scan
OK
<3>CTRL-EVENT-SCAN-STARTED 
<3>CTRL-EVENT-SCAN-RESULTS 
> scan_results
bssid / frequency / signal level / flags / ssid
00:1e:42:3b:18:d8	5180	-64	[WPA2-PSK-CCMP][ESS][UTF-8]	RUT_18D8_5G
a0:b5:49:05:70:51	5280	-56	[WPA2-PSK-CCMP][WPS][ESS]	nrb-99885
78:29:ed:53:06:94	5540	-61	[WPA2-PSK-CCMP][WPS][ESS]	nrb-99885
a0:b5:49:05:70:54	2412	-53	[WPA2-PSK-CCMP][WPS][ESS]	nrb-99885
84:a1:d1:33:f2:e9	5540	-74	[WPA2-PSK-CCMP][WPS][ESS]	Sunrise_5GHz_33F2E0
86:a1:d1:33:f2:e9	5540	-74	[WPA-PSK-CCMP+TKIP][WPA2-PSK-CCMP+TKIP][WPS][ESS]	Sunrise_TV_33F2E0
a0:b5:49:ac:ea:b0	5540	-77	[WPA2-PSK+SAE-CCMP][SAE-H2E][WPS][ESS]	xuk-21807
ac:22:05:7f:b9:a8	5220	-81	[WPA-PSK-TKIP][WPA2-PSK-CCMP][WPS][ESS]	UPCAC38844
84:a1:d1:33:f2:e4	2462	-70	[WPA2-PSK-CCMP][WPS][ESS]	Sunrise_2.4GHz_33F2E0
84:d8:1b:11:cf:50	2472	-73	[WPA2-PSK-CCMP][WPS][ESS]	CIA_Surveillance_Van
e2:30:ab:23:18:8b	2447	-74	[WPA2-PSK-CCMP][WPS][ESS]	Hondista
84:d8:1b:11:cf:4f	5180	-90	[WPA2-PSK-CCMP][WPS][ESS]	CIA_Surveillance_Van
00:1e:42:3b:18:d7	2437	-46	[WPA2-PSK-CCMP][ESS][UTF-8]	RUT_18D7_2G
bc:10:2f:1b:e4:90	2412	-82	[WPA2-PSK-CCMP][ESS]	Samsung Fridge_E50AJTRB087D
>
```
