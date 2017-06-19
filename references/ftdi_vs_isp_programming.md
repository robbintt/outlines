## FTDI v ISP v UART v SPI

FTDI is one implementation of UART. 

ISP is a set of different protocols based on the company.




### SPI - Serial Peripheral Interface

Wikipedia: [SPI](https://en.wikipedia.org/wiki/Serial_Peripheral_Interface_Bus)

Single Channel Simplex Communication

I used SPI via Raspberry Pi (original) GPIO pins to program a flash chip that I soldered onto my lenovo x220 mainboard to install coreboot.

#### Software

1. `flashrom`


### ISP/ICSP - `In-system Programming` or `In Circuit Serial Programming`.

Wikipedia: [ISP/ICSP](https://en.wikipedia.org/wiki/In-system_programming)


This allows you to program on-chip. There are multiple incompatible ISP technologies.

`AVR ISP` is very popular right now.

Wikipedia states: "A ISP USB cable must typically be shorter than 180cm"


### UART - `Universal Asynchronous Receiver/Transmitter`

Wikipedia: [UART](https://en.wikipedia.org/wiki/Universal_asynchronous_receiver/transmitter)



### FTDI is UART

`Future Technology Devices International` is a company

This is a UART implementation.

A number of FTDI programmers exist but do not always seem branded as such.

FTDI is apparently a company that people don't like. To use FTDI you need a 512 byte bootloader.


#### Arduino: FTDI or ISP?

Arduinos used to have an FTDI chip but it was too expensive so they moved to a second chip that can do USB ISP on the primary chip.


#### FTDI Programmers

1. Sparkfun FT232RL Breakout: [3v3](https://www.sparkfun.com/products/9873) [5v](https://www.sparkfun.com/products/9716)
    - These are called 'USB to serial IC' boards
    - These use miniUSB, there is a different offering for microUSB
    - Offers `DTR` pin but not `RTS`; `DTR` resets your arduino; other models offer `RTS`

1. Adafruit FTDI Friend FT232RL Breakout: [3v3 and 5v](https://learn.adafruit.com/ftdi-friend)
    - Offers `RTS` pin and `DTR` as a pad [DTR guide](https://learn.adafruit.com/ftdi-friend/programming-blank-avrs)
    - Offers 3v3 and 5v - signal is 3v3 (5v compatible), power is 5v... make sure you know what you are doing

#### Other brands

1. The ESP8266 AiThinker Light Bulb apparently needs an FTDI programmer
    - recommended by the developer: [AiLight Jig](https://www.sachatelgenhof.nl/blog/ailight-jig)
    - He got some boards from china, I have asked him for a link to the seller


### Raspberry Pi

How does this fit into the picture? I have used it with `flashrom` as a flash programmer for a lenovo x220 with a test clip, how is this related to everything else?


### The BUS Pirate

Apparently the BUS Pirate can do all of this, but requires configuration.


### Popular Software

1. avrdude
1. flashrom
1. arduino IDE
1. 
