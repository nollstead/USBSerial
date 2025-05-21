# USB-to-Serial Adapter

![USB2SerialAdapter](/images/U2SFront.png)

## Product Overview

Looking to breadboard your next MCU-based idea and need a USB or Serial interface to load firmware, voltage regulation and/or logic level conversion but annoyed with the hassle of using multiple components?  Well look no further - this USB-to-Serial Adapter is an easy to use, multi-function, breadboard friendly and feature rich USB-C breakout board, 5v-to-3.3v voltage regulator and Serlal/TTL adapter (with logic level conversion) all in one package.

This adapter fits perfectly on a breadboard and connects to your computer via a USB-C connector, allowing you to convert USB signals to Serial for programming various MCU's.  You can choose a target voltage of either 3.3v or 5v but unlike other products on the market the selection is done via a jumper pin - so no soldering required.

Both push-pull and open source driven DTR are supported, so this can be used a wide selection of MCUs.  Simply connect a 4.7kΩ resistor across CTS# and DTR# for push-pull driven DTR (e.g., ATMega328P targets) or a 4.7kΩ resistor from DTR# to GND for MCU's that require open source driven DTR.  Alternatively, there are spaces on the [back](/images/U2SBack.png) of the board to solder on a 1206 size resistor should that be preferred.

## Features & Specs

- Exposes both raw (VBUS) and filtered 5V from USB as well as 3.3v via an internal LDO voltage regulator.
- Exposes USB D+ and D- differential pairs with onboard ESD protection.
- Supports both push-pull and open source driven DTR
- Power, TX and RX LED's
- Automatic level shifting of serial signals to either 5v or 3.3v logic based on jumper selection
- ESD protection on USB connector
- 2mm holes for adding to an enclosure


## USB Breakout

The raw USB VBUS signal and D+/D- differential pairs are broken out as well as a cleaned up 5v signal filtered through an LC network.  The board contains the necessary 5.1kΩ resistors on the USB CC1 and CC2 pins to allow it to source power, so no need to expose them or add those resistors to your breadboard.

## Voltage Regulation

The onboard voltage regulator steps the 5v USB signal to 3.3v and exposes it via a pin.  So even without using any of the other features it can serve as a standalone USB5V-to-3V3 LDO voltage regulator.

## USB-to-Serial Conversion

USB-to-Serial conversion is accomplished by an onboard [CH340X](/ch340.pdf) and supports both 3.3v and 5v targets.  Select the desired output (VCC) voltage via the jumper pin and the serial signals are automatically level shifted accordingly.  

### DTR# Modes
To support as many target MCUs as possible, the DTR# pin can operate in one of three modes:  TNOW, push-pull driven DTR# and open source driven DTR#.  

- TNOW (default):  The DTR# pin functions as a transmit-now (TNOW) signal, typically used for half-duplex transceiver switching.  This mode is useful when working with RS485 communication, where the device needs to switch between transmitting and receiving data
- Push-Pull driven DTR:  Push-pull mode is activated by placing a 4.7KΩ resistor across the DTR# and CTS# (or solding a 1206 4.7KΩ on the back).  Push-Pull mode is useful when interfacing with microcontrollers that require a strong signal to control boot mode or reset signals - such as an ATMega328P or STM32F4
- Open Source Driven DTR:  Open source mode is activated by placing a 4.7KΩbpull-down  resistor on the DTR# pin.  In this configuration, the DTR# pin behaves as an open-drain output, meaning it can pull low but requires an external pull-up resistor to drive high. 

## Pinout

| Pin Name          | Pin Type  | Pin Description                |
| :----------- | :----------- | :------------------------- |
| VBUS      | POWER | The raw unfiltered 5v output from the USB connector.   |
| 5V        | POWER | The 5v USB output after going through a LC filter to remove noise inherent in USB power signals.  |
| 3V3      | POWER | 3.3v output of the onboard LDO voltage regulator |
| VCC      | POWER | Either 3.3v or 5v, depending on jumper pin selection.  Intended as primary voltage output to match target MCU when using as a USB to Serial converter |
| GND      | POWER | Common ground |
| CTS#    | IN | Clear to Send, active low(high) |
| DTR#    | IN | Data terminal ready that can opeate in one of two modes.  Connect a 4.7kΩ pull-down resistor for open source DTR enhanced mode or a 4.7kΩ resistor between DTR# and CTS# for push-pull DTR enhanced mode.  Note that the resistor can be either external or utilize one of the 1206 pads on the back of the board.  |
| RTS#      | OUT | Request to send |
| D-      | USB Signal | Direct USB D- signal with no series resistor |
| D+      | USB Signal | Direct USB D+ signal with no series resistor |
| TXO      | OUT | Serial transmit.  Logic level matches jumper selection and VCC   |
| RXI      | IN | Serial Receive. Logic level matches jumper selection and VCC |


## Documentation & Hookup Guides

- [Loopback Test](/loopback.md) - Here we'll cover the basics of connecting the adapter to your computer and performing a simple loopback test using a terminal emulator.
- [Hello World with ATMega328p](/HelloATMega.md) - With the basics under our belt, let's do something more interesting.  Here we'll demonstrate how to send and receive serial text using the Arduino IDE and a simple ATMega328P on a breadboard.