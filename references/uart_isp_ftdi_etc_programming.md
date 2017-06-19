# FTDI v ISP/ICSP v UART/USART v SPI

These terms cause a bunch of confusion.


## Bootloaders

It is popular to put a bootloader on your chip. This takes up some space but allows the chip to "reprogram" itself by writing to its own flash.

Some systems have a separate ISP/ICSP or UART chip on board and you can use that to reprogram the chip without a bootloader.

The purpose of both of these systems is that you can reprogram the chip while it is on-board.


## Disambiguation

FTDI is one implementation of UART. 

ISP/ICSP is a set of similar protocols created by different companies, AVR ISP is used with AVR chips and is common/popular.

UART is common. USART is uncommon. Many devices support UART and not USART. USART is similar to SPI.


### Definitions

- *asynchronous* - uses no clock
- *synchronous* - uses a clock


### Synchronous

- USART 
- SPI
- ISP/ICSP


### Asynchronous

- UART (therefore FTDI)


### References

1. Thread on [USART v SPI](https://electronics.stackexchange.com/questions/55960/difference-between-miso-mosi-and-txd-rxd)
1. Wikipedia
    - [SPI](https://en.wikipedia.org/wiki/Serial_Peripheral_Interface_Bus)
    - [ISP/ICSP](https://en.wikipedia.org/wiki/In-system_programming)
    - [UART](https://en.wikipedia.org/wiki/Universal_asynchronous_receiver/transmitter)


### SPI - Serial Peripheral Interface

Direction: Simplex

Channels: 1

I used SPI via Raspberry Pi (original) GPIO pins to program a flash chip that I soldered onto my lenovo x220 mainboard to install coreboot.


### ISP/ICSP - `In-system Programming` or `In Circuit Serial Programming`.

Direction: 

Channels: 

This allows you to program on-chip. There are multiple incompatible ISP technologies.

`AVR ISP` is very popular right now.

Wikipedia states: "A ISP USB cable must typically be shorter than 180cm"


### UART - `Universal Asynchronous Receiver/Transmitter`

Direction: Simplex, Half Duplex, Full Duplex

Channels: 1+ (typically 1 channel)

The foundation of UART is the shift register and clock.


#### Raspberry Pi <-> Arduino via UART

Note that in the demo, a `voltage divider` is used to talk from the arduino to the raspberry pi. The raspberry pi uses 3v3 on the UART tx/rx pins.  The arduino pin 11 (MOSI) gets the voltage divider to the Raspberry Pi GPIO 16 RxD UART.

- [Demo](http://radiostud.io/understanding-raspberrypi-uart-communication/)


#### What about Raspberry Pi -> ESP8266EX?

- Maybe the Raspberry Pi would be a good way to program the ESP8266EX?


## FTDI is UART

Direction: 

A common chip in 2017 is `FT232RL` which goes USB to UART.

The ESP8266EX AiLight uses the [BoyaMicro 25Q32ASSIG Chip] as an ISP.

`Future Technology Devices International` is a company that apparently makes people sad sometimes.

To use FTDI you need a 512 byte bootloader.

A number of FTDI programmers exist but do not always seem branded as such.


### Arduino: FTDI or ISP?

Arduinos used to have an FTDI chip but it was too expensive so they moved to a second chip that can do USB ISP on the primary chip.


### UART (FTDI) Programmers

1. Sparkfun FT232RL Breakout: [3v3](https://www.sparkfun.com/products/9873) [5v](https://www.sparkfun.com/products/9716)
    - These are called 'USB to serial IC' boards
    - These use miniUSB, there is a different offering for microUSB
    - Offers `DTR` pin but not `RTS`; `DTR` resets your arduino; other models offer `RTS`

1. Adafruit FTDI Friend FT232RL Breakout: [3v3 and 5v](https://learn.adafruit.com/ftdi-friend)
    - Offers `RTS` pin and `DTR` as a pad [DTR guide](https://learn.adafruit.com/ftdi-friend/programming-blank-avrs)
    - Offers 3v3 and 5v - signal is 3v3 (5v compatible), power is 5v... make sure you know what you are doing


#### Other brands

1. The ESP8266 AiThinker Light Bulb needs an UART programmer
    - recommended by the developer: [AiLight Jig](https://www.sachatelgenhof.nl/blog/ailight-jig)
    - He got some boards from china, I have asked him for a link to the seller


## Hardware

1. *JTAG Programmers* - Apparently the industry standard. Can we make these for fun?
2. [AVR ISP Programmers](http://www.ladyada.net/learn/avr/programmers.html)
3. Standard issue microcomputers
    - Raspberry Pi
    - Arduino Uno
    - BusPirate

### The *CP210x* USB to UART from Silicon Labs exists

It is cheaper than the FTDI FT232RL.

Adafruit offers this chip and it is also in other popular USB->UART devices.


### Raspberry Pi

How does this fit into the picture? I have used it with `flashrom` as a flash programmer for a lenovo x220 with a test clip, how is this related to everything else?


### BusPirate

Apparently the BUS Pirate can do all of this, but requires configuration.


### Arduino Uno

Careful! Transmits at 5V which will fry the Raspberry Pi and esp8266.


## Software

1. `flashrom`
2. `avrdude`
3. `Arduino IDE`


