## Openwrt for DOVADO PRO-AC

#### Hardware Info

| - | - |
| ------------- |:-------------:|
| **Architecture** | MIPS |
| **Vendor** | Mediatek |
| **Bootloader** | U-Boot |
| **SOC** | MT7621ST |
| **CPU/Speed** | mipsel_24kc @ 880MHz |
| **Flash chip** | MX25L12835F / 16MB | 
| **RAM** | W971GG6SB-25 / 128MB |
| **WIFI 2.4 GHz** | MT7603EN, b/g/n |
| **WIFI 5 GHz** | MT7612EN, a/n/ac |
| **Ethernet** | 5x 10/100/1000 BASE-TX Ethernet Interface (1x WAN, 4x LAN) |
| **USB** | 2x (1x USB2.0, 1x USB3.0) |
| **Serial** | ? |
| **JTAG** | ? |

#### Flashing

For installing OpenWrt there are the following methods:

* **Using SPI chip programmer** (Requires extra hardware): writting full firmware eeprom dump directly to the SPI flash chip.
* U-Boot(?): Seems u-boot is locked/performing some sort of firmware check before flashing, I was unable to flash using TFTP. Need serial connection to figure out what's going on there.

##### Flashing using SPI programmer

1. Disassemble the device
2. Connect SOIC-8 clip to the flash chip (located at the bottom side of the main board)
3. Plug in SPI programmer (I'm using cheap CH341A USB)
4. Power on the router (Well, I have to do this because without being powered on device draws too much power so flashing (erasing/writting) will most probably fail)
5. Flash openwrt dump to the device:
`sudo flashrom -p ch341a_spi -c "MX25L12835F/MX25L12845E/MX25L12865E" -w openwrt-21.02.1-dovado_proac.bin`
6. Reboot the device. Connect to http://192.168.1.1

Openwrt sysupgrade works OK, so you can build your own image and flash it safely using Openwrt UI. See build config and device support patch in this repo.

21.12.21 faust93

