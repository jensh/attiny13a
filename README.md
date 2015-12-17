Core13a
=======

This is a fork of Core13. An Arduino core for Attiny13.

http://sourceforge.net/projects/ard-core13/

The initial commit comes from core13_022_arduino_1_6.zip

It supports the ATtiny13 successor ATtiny13a with new Bits and
registers (e.g. BODCR and PRR).


For other ATtiny variants take a look at

https://github.com/damellis/attiny


A good collection of other Arduino AVR projects for the Arduino IDE:

http://playground.arduino.cc/Main/ArduinoOnOtherAtmelChips


Installation
============

Cd to your Arduino "hardware" folder inside your Arduino
installation and clone this repository into it:

e.g.
```
cd /opt/arduino/arduino-1.6.6/hardware
git clone https://github.com/jensh/attiny13a.git
```

Start/restart the Arduino IDE afterwards. You should now have a new
entry in "Tools / Board" "ATtiny13A". If chosen, you can select the
configured cpu frequency in "Tools / CPU Frequency". This will not
change the fuses! It only tells the compiler which F_CPU macro to use
for delay calculations. The factory default is 1.2MHz (= 9.6MHz/8,
CKDIV8 programmed).


CPU Frequency / Fuses
=====================

To change the fuses, select the right programmer
"Tools / Programmer / USBasp for ATtiny13a" and execute "Tools / Burn
bootloader" (currently not working!).

Or use avrdude on the command line. Attention! :warning: A wrong setting might
disallow further serial programming via SPI! This brick your tiny
unless you own a high voltage programmer (HVSP) (see below)!

```
# (:warning: Needs high voltage programming for reset! HVSP)
# 16kHz with CKDIV8=1, 128kHz/8 und 14CK + 64ms Startup
avrdude  -v -pattiny13 -cusbasp -Pusb  -Uhfuse:w:0xFF:m -Ulfuse:w:0x6B:m

# 128kHz with CKDIV8=1, 128kHz und 14CK + 64ms Startup
avrdude  -v -pattiny13 -cusbasp -Pusb  -Uhfuse:w:0xFF:m -Ulfuse:w:0x7B:m

# 600kHz with CKDIV8=0, 4.8MHz/8 und 14CK + 64ms Startup
avrdude  -v -pattiny13 -cusbasp -Pusb  -Uhfuse:w:0xFF:m -Ulfuse:w:0x69:m

# Default: 1.2MHz with CKDIV8=0, also 9.6MHz / 8 14CK + 64ms Startup
avrdude  -v -pattiny13 -cusbasp -Pusb  -Uhfuse:w:0xFF:m -Ulfuse:w:0x6A:m

# 4.8MHz with CKDIV8=1, 4.8MHz und 14CK + 64ms Startup
avrdude  -v -pattiny13 -cusbasp -Pusb  -Uhfuse:w:0xFF:m -Ulfuse:w:0x79:m

# 9.6MHz with CKDIV8=1, 9.6MHz und 14CK + 64ms Startup
avrdude  -v -pattiny13 -cusbasp -Pusb  -Uhfuse:w:0xFF:m -Ulfuse:w:0x7A:m
```

Maybe helpfull to recover from wrong fuse settings is Wayne's: "ATTiny
Fuse Reset"
https://sites.google.com/site/wayneholder/attiny-fuse-reset


License
=======

Most sourcefiles are "GNU Lesser General Public", some are less
restrictive. Take a look in the particular sourcefile!
