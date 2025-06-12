# Bare Bones ATMega328P

In our [previous example](/HelloATMega.md) we added the USB Buddy to a breadboard along with a commercial Arduino Pro Mini.  That's interesting but let's take it up a notch.  Suppose you're really interested in building your own ATMega328P-based board and just need a way to load a sketch without all of the fuss.  In this example we'll build our own Arduino Uno from scratch, supply it with it's own power and use the USB Buddy externally to load a sketch.  Let's see what that looks like

For this example you'll need the following components
- A USB Buddy
- A [USB-C cable](https://www.sparkfun.com/usb-3-1-cable-a-to-c-3-foot.html)
- A [breadboard](https://www.sparkfun.com/breadboard-full-size-bare.html) and a [male-to-male jumper wires](https://www.sparkfun.com/jumper-wires-premium-6-m-m-pack-of-10.html)
- A [Solderless Breadboard Power Supply Module](https://www.amazon.com/dp/B08JYPMCZY?ref_=ppx_hzsearch_conn_dt_b_fed_asin_title_15&th=1) set to 5v
- a 9V battery
- [Arduino Kit](https://www.amazon.com/dp/B0BQSD1HHV?ref=ppx_yo2ov_dt_b_fed_asin_title).  
- An [Atmega328P-PU microcontroller](https://www.ebay.com/itm/195491240929?var=495358594463)
- [Pin Headers](https://www.sparkfun.com/header-pins-14x1.html)
- a [4.7kΩ resistor](https://www.amazon.com/dp/B09PLNPX3P?ref_=ppx_hzsearch_conn_dt_b_fed_asin_title_2&th=1)

## Microcontroller Selection

In order to respond to serial programming commands, the ATMega328p needs a bootloader (as well as the appropriate FUSE bits set).  When purchasing an ATMega328p, most come without a bootloader but you can find some that have them preinstalled - albeit more expensive.  To keep things simple, for this example we'll use the one listed above - which is a kit that includes not only the MCU but all of the other components needed to get it working - including a crystal, resistors, capacitors and even a button and LED.  

If you choose to use your own ATMega328p chip you'll either need to get one with a bootloader or add the bootloader yourself, as well as the following items in addition to the ones listed above:
- A [16MHz crystal](https://www.amazon.com/dp/B07Y7GFVGX?ref_=ppx_hzsearch_conn_dt_b_fed_asin_title_2)
- Two [22pf capacitors](https://www.amazon.com/ALLECIN-Capacitors-Multilayer-Monolithic-Capacitor/dp/B0DFQ9K817/ref=sr_1_2_sspa?crid=VB2WHZMYMFMI&dib=eyJ2IjoiMSJ9.YvrY2r1mtGosktZVqGjBWWNp_MMJZLUapnPbj0bjvDDH5S3EDnYrsui6MLZqp_K6uVRvS0vnhv7KE3rWMj7pL6v1g6iIxLnAPNkR4XDeua2_n1x7LhhVi0sB98UVCbrZijkZ3GHZG5Zrkoyf3nfQ_30G-wEfTqSrtqVUtARleHC8CjycN1u_Ljco08247OHziK1Uck0laBMKp7zPL9ZLpXBj0fAkk18Z5-T5RWKf1e0.ulTJwXHyHwJe_D0o2heGTjwn0-BOukLlXDZe7hcZYNY&dib_tag=se&keywords=22pf%2Bcapacitor&qid=1748495565&sprefix=22pf%2Bcap%2Caps%2C88&sr=8-2-spons&sp_csd=d2lkZ2V0TmFtZT1zcF9hdGY&th=1).  
- a [10kΩ resistor](https://www.amazon.com/dp/B09PLNPX3P?ref_=ppx_hzsearch_conn_dt_b_fed_asin_title_2&th=1)
- [Three 100nF (0.1uF) capacitors and one 10uF capacitor](https://www.amazon.com/dp/B085RDTCCV?ref_=ppx_hzsearch_conn_dt_b_fed_asin_title_1&th=1)
    Note: The 10uF capacitor and two of the 100nF capacitors are optional but best practice to include



## 1. Wiring it all up

1. Turn the adapter over and solder the header pins to the bottom, so that the longer ends extend up and solder the 4.7kΩ resistor to the pads on the bottom aligned with 'push-pull driven DTR'.  In this example we won't attach the adapter to the breadboard, but we'll still need access to the pins.
2. Move the jumper on the adapter to the 5v position if not already there.
3. Add the power supply module to the breadboard and set both jumper pins to 5v.  Be sure to match up the + and - sides to the red and blue sections, respectively - just to avoid confusion.
4. Add the ATMega328P to the breadboard with pin 1 facing the power module.  Pin 1 corresponds to the left pin on the end of the chip with the notch.  Refer to [this diagram](https://www.bitfoic.com/upload/20231213/25844c0c0e8684550735d6f25012063d.jpg) for a pinout reference and numbering.
5. Connect the crystal to pins 9 and 10 on the AtMega328P and connect pins 9 and 10 to gnd using a 22 pF capacitor on each line.
6. Connect both pins 9 and 10 to GND with a 22pF capacitor
7. Connect pin 7 to the power rail and a also a 100nF capacitor from pin 7 to the power rail
8. Connect pin 20 to the power rail and a also a 100nF capacitor from pin 20 to the power rail
9. Connect pins 8 and 22 to the GND rail
10. Connect pin 1 to the power rail through a 10kΩ resistor
11. Connect a 10uF capacitor across the power and gnd rails. This be anywhere on the breadboard, not necessarily right next to the ATMega328 (though it should be relatively close if using a large breadboard)
12. Connect a F/M jumper from the GND pin on the adapter to either GND rail on the breadboard
13. Connect a F/M jumper from the RXI pin on the adapter to pin 3 on the ATMega328P
13. Connect a F/M jumper from the TXO pin on the adapter to pin 2 on the ATMega328P
14. Connect a 100nF capacitor to pin 1 on the ATMega328p and any open rail on the breadboard. Then F/M jumper from that rail to the DTR pin on the adapter.

## 2. Loading a 'Hello World' Sketch

Now that everything is wired up it's time to test it with a simple sketch.  This time we'll use the button that came in the kit to toggle the LED and print a message to the serial window.  Open the Arduino Ide and replace the default code with the code below and press Upload (right arrow button).  

```arduino
#define BUTTON_PIN 9

bool previousButtonState = HIGH;    // Button starts off as HIGH due to INPUt_PULLUP

void setup() {
    pinMode(LED_BUILTIN, OUTPUT); // Set LED pin as output
    pinMode(BUTTON_PIN, INPUT_PULLUP);
    Serial.begin(115200); // Start serial communication at 9600 baud
}

void loop() {
  
  bool currentState = digitalRead(BUTTON_PIN); // Read button state

    if (currentState == LOW) { // Button is pressed
        digitalWrite(LED_BUILTIN, HIGH); // Turn LED on
        
        if (previousButtonState == HIGH) { // Only say hello once
            Serial.println("Hello, world!");
        }
    } else {
        digitalWrite(LED_BUILTIN, LOW); // Turn LED off
    }
    previousButtonState = currentState; // Update for next loop iteration
}
```
<!-- 
## Command Reference

### Reading fuses using a programmer (can't do usign serial)
```
avrdude -C..\..\..\..\tools\avrdude\6.3.0-arduino18/etc/avrdude.conf -P COM13 -c arduino -b 19200 -p m328p -v
```

### Setting fuses using a programmer
```
avrdude -C..\..\..\..\tools\avrdude\6.3.0-arduino18/etc/avrdude.conf -P COM13 -c Arduino -b 19200 -p m328p -U lfuse:w:0xFF:m -U hfuse:w:0xDE:m -U efuse:w:0xFD:m -v
```
 -->
