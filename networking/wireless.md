# Wireless Networking

There are 4 common types of wireless networks:

### PAN - Personal Area Network
Never really thought about it but when you're using Bluetooth you're essentially
setting up a mini personal LAN.  The term for this is PAN! :-)

### LAN - Local Area Network (WiFi)
Network within your home or business.

### MAN - Metropolitan Area Network (WiMAX)
City wide network

### WAN - Wide Area Network (Celluar/UMTS/LTE, etc.)
Worldwide network

**Channel Capacity** - is the maximum information rate of any of these networks
measured in bits/s.

`C = BW X log2 (1 + S/N)`

The main constraints being 1. bandwidth and 2. signal power between receiver and
sender.

### Bandwidth

All these networks rely on selecting a pre-determined range for their
electromagnetic radiation (radio waves).  The ranges are generally determined by
the government.  Because of this, some countries may assign different ranges to
the same wireless tech!

### Signal Power

Think about having a conversation with friend at a party.  If they're far away
you have to yell but then everyone has to start yelling.  Soon, everyone is
yelling and everyone needs to be close.  It's generally more effective to just
move closer to the person you're trying to communicate with.  This is a great
analogy to SNR (aka S/N ratio, aka signal-power-to-noise-power).

### Modulation
Is the process of converting binary into radio alphabets.  Turning digital to
analog.  There are various algorithms that do this better and worse.

Example:
* receiver/sender can process 1,000 pulses (or symbols) per second... 1000 baud
* each symbol represnts a different 2-bit sequence (00, 01, 10, 11)
* the bit rate of the channel is 1000 baud X 2 = 2000 bits/s


### LTE - Long Term Evolution 
