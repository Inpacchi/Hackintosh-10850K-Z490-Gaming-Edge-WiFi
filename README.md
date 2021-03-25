# Hackintosh-10850K-Z490-Gaming-Edge-WiFi
Hackintosh build for an i9-10850K on an MSI MPG Z490 Gaming Edge Wi-Fi

## Major Versions
- OpenCore v0.6.7
- macOS Catalina 10.15.7

## [Build Specs](https://pcpartpicker.com/list/9b7GYg)
- Intel Core i9-10850K
- Arctic Liquid Freezer II 360
- MSI MPG Z490 Gaming Edge Wi-Fi
	- Audio: Realtek ALC1200-VD1
	- LAN: Realtek RTL8125B 2.5G
  - Wireless Card & Bluetooth: Intel AX201
- 4x8GB (32GB) Corsair Vengeance RGB 3200Mhz CL16
- PowerColor Red Devil Radeon RX 5700 XT

## What's tested and working?
- iServices
- Audio
- Wi-Fi & Bluetooth
  - Wi-Fi works with the itlwm.kext found [here](https://github.com/OpenIntelWireless/itlwm)<sup>1</sup> but read into this a bit more; it requires you to hardcode the SSID and password OR use HeliPort to gain Wi-Fi access.
  - I did NOT test AirportItlwm.kext.
  - Bluetooth works with the included kexts.
- LAN
  - The kext for our LAN adapter does not auto-negotiate and thus needs to be manually set to 1000baseT.
- USB
  - Some ports are disabled due to macOS's 15 port limit; this is explained further down.
- Native CPU power management
- Sleep/Wake, Restart, Shutdown

<sup>1: I have not included the itlwm.kext in this EFI setup as I don't need it.</sup>

## Issues Encountered During Installation & Setup
- You can't install macOS without a network connection, so you have to use the terminal to set the negotiation speed.
  - `ifconfig en0 media 1000baseT` should typically take care of this.
- I had this nagging issue where the installer would crash back to the start screen after I select a disk. I found this issue by looking in the installer log and found the line `No mapping for user data read` which, upon some Googling, revealed USB and port issues. Unfortuantely I didn't have macOS installed so I wasn't sure how to fix this...so I disabled all but two ports in the BIOS and found out which ports were still enabled by trial and error. I used a USB Hub for my installation media, keyboard and mouse and it installed without a hitch.
- My current issue is that the system will essentially crash (speaker starts making a buzzing noise, cursor turns pixelated and the system stops responding.) Some Googling shows that this might be due to my overclocked RAM. I didn't think this at first because my original overclock was stable on Windows, but it figures that it'd be different on a Hackintosh (I mean, duh, right?) Currently have it toned down a notch and testing.

## Important Notes
- I pretty much followed the [Dortania Guide](http://dortania.github.io) to a tee
- Using USBMap, I disabled ports I deemed non-essential to my needs - which were my front USB ports.

## Overclock Settings
### Baseline CPU
- Settings: Everything stock/auto in BIOS
#### Cinebench R23
- Score: 16,360
- Temperature: 65-70 celsius average, 71 celsius peak
#### [Geekbench](https://browser.geekbench.com/v5/cpu/7117150)
- Single-Core Score: 1319
- Multi-Core Score:11,604
- Temperature: 36 celsius average during less intensive calculations; 60-65 celsius average during more intensive calculations

### Overclocked CPU
- Settings: 5.1GHz All-Core @ 1.33v, LLC mode 4
#### Cinebench R23
- Score: 17,297
- Temperature: 87 celsius average, 88 celsius peak
#### [Geekbench](https://browser.geekbench.com/v5/cpu/7118227)
- Single-Core Score: 1333
- Multi-Core Score: 12,192
- Temperature: 38 celsius average during less intensive calculations; 72-80 celsius average during more intensive calculations
#### Notes
I tried LLC mode 2 but saw peaks of 92 celsius and an average of about 89-90 celsius. It was much more stable temperature-wise on LLC mode 4.
  
### RAM
- 3600 @ 1.35v, 14-14-14-34
- Stress tested using macOS version of memtest
