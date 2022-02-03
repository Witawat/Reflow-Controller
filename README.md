# Reflow-Controller

**This page is a work in progress!**

The Reflow-Controller was built to control different kinds of reflow ovens, hotplates and whatever is coming to my mind in the future. It is based on the ESP32-S2 ([datasheet](https://www.espressif.com/sites/default/files/documentation/esp32-s2_datasheet_en.pdf)) and thus can be programmed to be used with a WiFi App or whatever. Nevertheless, it has an onboard OLED display and three buttons included to be used as a standalone solution either.

Features of the PCB:

- ESP32-S2 MCU
- 2x MAX6675 thermocouple sensor input
- 2x Fan output (inductive loads/flyback diodes included)
- 2x Solid state relay output
- 3x User button
- 1x APA102 user LED
- 1x Buzzer
- 1x Servo motor output
- 0,96" OLED display
- Optional ACDC converter (HLK-PM05, HLK-PM12) which can be separated if not used
- Optional I2C (QWIIC) connector


## GPIOs

The ESP32-S2 is connected like this:

Function | GPIO | Mode
-------- | -------- | --------
SSR1 | GPIO1 | Output
SSR2 | GPIO2 | Output
Servo | GPIO3 | Output
Fan1 | GPIO5 | Output
Fan2 | GPIO6 | Output
CLK | GPIO7 | SPI
MISO | GPIO9 | SPI
MOSI | GPIO11 | SPI
CS1 | GPIO12 | SPI
CS2 | GPIO13 | SPI
Buzzer | GPIO15 | Output
USB D- | GPIO19 | CDC
USB D+ | GPIO20 | CDC
SDA | GPIO33 | I2C
SCL | GPIO35 | I2C
Button1 | GPIO36 | Input
Button2 | GPIO39 | Input
Button3 | GPIO40 | Input
LED CLK | GPIO37 | LED
LED DATA | GPIO38 | LED
OLED RST | GPIO45 | Output

## ACDC power supply

The upper part of the PCB can be used as a power supply for the whole board as well as the higher voltage outputs (SSRs, Fans). If not used, it can be separated from the main board and may be used in another project where an ACDC adapter is needed.

The main board is equipped with an LM1117 3.3v voltage regulator which can be feed with 15v max. The output voltage of the ACDC power supply is the voltage for the SSR and the fan output channels. If you wanna use a servo motor in your project, make sure that the power supply has the correct voltage for the motor (probably 5v).

The HLK-PMXX module for the upper part of the PCB can be placed in two ways - on the bottom or on the top side. This gives the possibility to mount the whole PCB behind an acrylic glass (or whatever) so that the buttons as well as the OLED display are accessible. The two jumpers can then be used to select which signal is VCC and which one is GND. **Keep in mind that there are high voltage pins on the top side of the PCB when mounting the power supply on the bottom side! I've designed a 3D-printable cover, so that these pins cannot be touched accidentally. (Should be mounted in both cases)**

The board can also be powered via USB-C, but keep in mind that the output channels and the servo motor are not powered in this case (initially it is just available for flashing the board).


## Reflow Profiles
