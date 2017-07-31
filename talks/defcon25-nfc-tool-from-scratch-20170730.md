## NFC Tool From Scratch


Speaker: shanhaoqi@360.cn
Location: Defcon 25 (2017)


- NFC & ISO14443A
- What is UniProxy
- Master and Slave


### Quick Demo I

Put the credit card in a UniProxy Master
1. Put the 

- 2 UniProxy Hardware
- 1 Cellphone
- 1 NFC enabled credit card


### Who we are: `Unicorn Team`

- Insternal security research team of Qihoo 360, founded in 2014.
- Focus on wireless hardware hacking and defense
- Low cost GPS Spoofing Defcon 23
- `LTE Redirection` acttac - Defcon 24
- Attack on powerline communication, Blackhat USA 2016
- `Ghost Telephonist` - Defcon 25


- Serial hacking tools developed: HackID, HackID Pro, SafeRFID - more I missed


### NFC and ISO14443A

We will focus on ISO14443A for the demo.

- NFC
	- 13.56MHz
	- low-cost
	- does not require power
	- well developed and deployed

- ISO14443A
	- In china: passport, bank card, etc.
	- more info in slides


### Goals

- ID Card	- could be exploited
	- Access forbidden area
	- Target banking systems

### How

- Targeting Protocols
	- Proxmark III (The best RFID hardware)
		- Supports many protocols, powerful, cannot hack credit cards
	- ChameleonMini
- Targeting Data: `NFCProxy`, `NFCGate`


#### What is UniProxy

Can be extended for ISO14443 protocol and 15693 standard.

- PN7462AU based NFC relay/proxy device
- Supports ISO14443A Protocol
	- Can be extended for other protocols that the chipset supports
- Targeting QuickPass, VisaPay, EMV, Unipay credit cards
- Reader emulator: Master 
- card emulator: Slave
- ... see photos

#### Why PN7462AU

- NXP Chip
- 20 MHz Cortext-M0 Core


##### 24L01 Chip coordinates between the master and slave

##### Their company has not open sourced the firmware, they didn't let him


#### I think they write some bits on the iblock and a lot of the iblock is boiler plate?

#### Lee says the nfc transaction times out easily and this might keep the connection warm?


### If there is an R block the card emulator will process itself



### Speaker says: Principle Described is "VERY SIMPLE"


### Issues

Tons of issues occurred in development.

- First byte of UID is in the firmware, will always be "zero eight"??
	- Did not find a way to modify?
- Waiting/Wakeup time
	- Real issue when developing a proxy tool
	- NFC has no power, uses power from the reader
	- Gets response from the reader and turns off
	- Must modify wakeup time - see code (to ensure the NFC is powered?)
- I/S/R - Block data
	- We do not need to transfer all data
	- Just transfer I block data, need to directly transfer S/R block data
	- Read the ISO carefully for more info
- Power supply can cause corruption of the chipset
	- Don't to do any tricks = follow the regular procedure
	- This is very sensitive

### The proxy card is used to make the purchase when the master card can be read

There is a video of the proxy card in action on my phone.



#### You should use a GuardBunny sleeve on your NFC cards to block RF...


#### Summary

1. Read Protocol Well
2. Better not develop without official support

#### Improvements - future

1. Improve transmission range to 100 meters
	- Currently 50? 15? meters
2. Target security ID cards, HID iClass, Chinese ID
3. Self-compatibility
	- Currently only ISO14443A
	- want to adapt to 15693 and let it know which it is using
4. How?


