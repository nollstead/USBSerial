# Hello ATMega

Here we'll demonstrate how to send and receive serial text using the Arduino IDE and a simple ATMega328P on a breadboard.  Instead of using an Arduino UNO (that would be too easy), we'll make our own on a breadboard

For this example you'll need the following components
- A [USB-C cable](https://www.sparkfun.com/usb-3-1-cable-a-to-c-3-foot.html)
- [Pin Headers](https://www.sparkfun.com/header-pins-14x1.html)
- A [breadboard](https://www.sparkfun.com/breadboard-full-size-bare.html) and a [male-to-male jumper wires](https://www.sparkfun.com/jumper-wires-premium-6-m-m-pack-of-10.html)
- An [ATMEGA328P-PU](https://www.ebay.com/itm/195491240929?var=495358594463) with a bootloader installed.
- A [4.7kΩ resistor and a 10kΩ resistor](https://www.amazon.com/dp/B09PLNPX3P?ref=ppx_yo2ov_dt_b_fed_asin_title&th=1)
- A [100nF (0.1uF) capacitor and a 10uF capacitor](https://www.amazon.com/dp/B085RDTCCV?ref_=ppx_hzsearch_conn_dt_b_fed_asin_title_1&th=1).  *Note:  the 10uF capacitor is optional but recommended
- A [16MHz crystal](https://www.amazon.com/dp/B07Y7GFVGX?ref_=ppx_hzsearch_conn_dt_b_fed_asin_title_1)

## 1. Wiring it all up

1. Add the adapter and the ATMega328P to the breadboard
2. Select the 5v option on the adapter by jumping the top and middle pins together
3. Connect the VCC pin on the adapter to the positive rail on the breadboard
4. Connect the GND pin on the adapter to the ground rail on the breadboard
5. Connect pin 22 on the ATMega328P to the ground rail


## 2. Loading a bootloader

For this example we need an ATMega328P that already has a bootloader installed.  There are online resources for learning how to do this, including an excellent tutorial from [DroneBot Workship](https://www.youtube.com/watch?v=Sww1mek5rHU&t=1203s).  Alternatively you can check out our [ICSP Programmer](https://github.com/nollstead/icsp)
