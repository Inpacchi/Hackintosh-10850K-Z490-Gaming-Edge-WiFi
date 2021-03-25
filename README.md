# Hackintosh-10850K-Z490-Gaming-Edge-WiFi
Hackintosh build for an i9-10850K on an MSI MPG Z490 Gaming Edge Wi-Fi

## Major Versions
- OpenCore v0.6.7
- macOS Catalina 10.15.7

## Build Specs
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
- My current issue is that the system will essentially crash (speaker starts making a buzzing noise, cursor turns pixelated and the system stops responding) which I have not been able to find a solution for.

## Important Notes
- I pretty much followed the [Dortania Guide](http://dortania.github.io) to a tee
- Using USBMap, I disabled ports I deemed non-essential to my needs - which were my front USB ports.

## Overclock Settings
### CPU
#### Cinebench R23
- Settings: 5.1GHz All-Core @ 1.32v, LLC mode 2
- Score: 17,184
- Temperature: 87 celsius averaege; 80-88 celsius average range
  
### RAM
- 3733 @ 1.35v, 16-18-18-38
- Stress tested using macOS version of memtest
