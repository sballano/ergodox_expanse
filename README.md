# ErgoDox Expanse

The ErgoDox Expanse is a DIY hand-wired version of the EdgoDox Infinity using the Teensy 3.2 board as the controller. The display used is a 128x64 OLED display with the SSD1306 controller instead of the Infinty LCD. RGB backlight support is planned but not yet tested.

The only keymap tested is the 'ballanux' one, intended for spanish layout, but any other ergodox keymap should work.

## Wiring instructions

This is the cabling that matches the configuration on the software. For easy wiring different color cables can be used. All the required cables can be obtained by scraping an old parallel port printer cable. Both sides of the keyboard are wired in the same way.

The wiring for master/slave communication between both sides is at the bottom table. Only the master side should be connected to the computer. To avoid supply issues between both sides it is recommended to put a diode between the 5V from the master and the 5V to the slave. An old USB cable could be cut and used for this purpose. It doesn't need to be shielded so a thin one can be used. The diode can be a 1N4148 or similar.

The current prototype doesn't have RGB backlighting, but it can be wired if desired as shown in Table 3. For this it is required to use a 'Neopixel led strip' (SK6812RGB) or similar and configure the software acordingly.


### Table 1. Key matrix wiring:

Matrix|uC Port|Teensy|Color
------|-------|------|-----
Col. 1|PTB2|PIN 19|Grey
Col. 2|PTB3|PIN 18|Brown
Col. 3|PTB18|PIN 32|White
Col. 4|PTB19|PIN 25|Blue
Col. 5|PTC0|PIN 15|Pink
Col. 6|PTC9|PIN 27|Green
Col. 7|PTC10|PIN 29|Purple
Col. 8|PTC11|PIN 30|Yellow
Col. 9|PTD0|PIN  2|Orange
Row. 1|PTD1|PIN 14|Brown/White
Row. 3|PTD5|PIN 20|Purple/White
Row. 2|PTD4|PIN  6|Black/White
Row. 4|PTD6|PIN 21|Yellow/Black
Row. 5|PTD7|PIN  2|Blue/White


Right side columns wiring:
![Right side columns wiring](https://i.imgur.com/VzcTDnk.jpg)

Left side rows and columns wiring:
![left side rows and columns wiring](https://i.imgur.com/J3Z6nuV.jpg)

Wiring to the Teensy controller:
![Wiring to the Teensy controller](https://i.imgur.com/gfvivOr.jpg)

Teensy detail:
![Teensy detail](https://i.imgur.com/jIaTpQs.jpg)


### Table 2. OLED display wiring:

SD1306|uC Port|Teensy|Color
------|-------|------|-----
CS|PTC4|PIN 10|Grey/Black
RST|PTC8|PIN 28|Green/Black
D/C|PTC7|PIN 12|Pink/Black
SCK|PTC5|PIN 13|Blue/Black
MOSI|PTC6|PIN 11|Light blue

OLED wiring:
![OLED wiring](https://i.imgur.com/tWrabMi.jpg)

OLED detail:
![OLED detail](https://i.imgur.com/bqqstJm.jpg)

### Table 3. RGB backlighting

SD1306|uC Port|Teensy|Color
------|-------|------|-----
+5V|---|Vin|Red
DIN|PTB18|PIN17
GND|GND|GND|Black


### Connection diagram from master to the slave:
```
                     1N4148
		+5V Master ---|>|---- +5V Slave 
		TX0 ----------------------- RX1
		RX0 ----------------------- TX1
		GND ----------------------- GND
```

### Table 4. Master/Slave wiring:

M.Signal|M.Port|M.Teensy|Color|S.Signal|S.Port|S.Teensy
--------|------|--------|-----|--------|------|--------
+5V|---|Vin|1N4148|+5V|---|Vin
TX0|PTB17|PIN 1|Green|RX1|PTE1|PIN 26
RX0|PTB16|PIN 0|Blue|TX1|PTE0|PIN 31
GND|GND|GND|Black	GND|GND|GND

Master/Slave connection working:
![Master/Slave connection](https://i.imgur.com/h3It6Bm.jpg)

## Firmware

The firmware for the keyboard is the QMK firmware, with the modifications required to make the Teensy 3.2 and the OLED display:

[https://github.com/sballano/qmk_firmware/](https://github.com/sballano/qmk_firmware/)

The firmware building and flashing instructions can be found at:

[https://github.com/sballano/qmk_firmware/tree/master/keyboards/ergodox_expanse](https://github.com/sballano/qmk_firmware/tree/master/keyboards/ergodox_expanse)

The original QMK repository can be found at:

[https://github.com/qmk/qmk_firmware](https://github.com/qmk/qmk_firmware)
