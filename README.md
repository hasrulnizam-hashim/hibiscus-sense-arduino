# Hibiscus Sense ESP32 Arduino Tutorial

<p align="center"><a href="https://myduino.com/product/myd-036/"><img src="https://github.com/myinvent/hibiscus-sense/raw/main/references/hibiscus-sense-logo.png" width="300"></a></p>
<p align="center"><a href="https://myduino.com/product/myd-036/"><img src="https://github.com/myinvent/hibiscus-sense/raw/main/references/hibiscus-sense.png" width="400"></a></p>

[Hibiscus Sense](https://myduino.com/product/myd-036/) is an Internet of Things (IoT) development board, powered by the mighty and popular dual-core [ESP32](https://www.espressif.com/en/products/socs/esp32) microcontroller, which on-board equipped with:
- 3 sensors:
  - **APDS9960**: an environment sensor, which sense *proximity, RGB* and *gesture*.
  - **BME280**: an environment sensor, which sense the *altitude, barometric pressure, humidity* and *temperature*.
  - **MPU6050**: 6-axis motion tracking sensor, which sense *3-axis gravitational acceleration, 3-axis rotational velocity* and *temperature*.
- 3 actuators:
  - **Buzzer**: short distance small buzzer.
  - **LED**: blue LED.
  - **RGB LED**: WS2812 RGB LED.

Comes with **USB Type-C** to powered the board with 5V and to program the ESP32 microcontroller, which on-board has USB-to-Serial converter **Silicon Labs CP2104** with **automatic bootloader reset**, so we don’t have to press the RESET button each time to upload the program into the microcontroller.

Despite, we can program ESP32 using other programming language and it's tools, in this tutorial we will focus on using [Arduino](https://www.arduino.cc/) as the learning and prototyping platform.

## Hibiscus Sense Features

<p align="center"><img src="https://github.com/myinvent/hibiscus-sense/raw/main/references/hibiscus-sense-features.png" width="900"></a></p>

## Hibiscus Sense Pinout Diagram

<p align="center"><img src="https://github.com/myinvent/hibiscus-sense/raw/main/references/hibiscus-sense-pinout.png" width="900"></a></p>

- **Blue LED** is connected to `GPIO2` ESP32 microcontroller.
- **Small Buzzer** is connected to `GPIO13` ESP32 microcontroller.
- **WS2812 RGB LED** is connected to `GPIO16` ESP32 microcontroller.
- All GPIO can generate digital input/output (3.3V) and PWM signal output, except `GPIO34-GPIO39` because it is an input pin only.
- ESP32 `VSPI` is complete **MISO** `GPIO19`, **MOSI** `GPIO32`, **CLK** `GPIO18` and **CS** `GPIO5`.
- ESP32 `I2C` **SDA** `GPIO21` and **SCL** `GPIO22`, without pullup resistor.
- **Sensors**: **APDS9960**, **BME280** and **MPU6050** interfaced to the `I2C` ESP32 microcontroller, respectively I2C address: `0x39`, `0x77` and `0x68`.
- Avoid to use `ADC2` channel while using WiFi.
- Each GPIO absolute maximum current drawn only 16mA.
- Board measurement including header in mm: 58.7 x 27 x 13.3 (length x width x height).
- Package measurement in mm: 71.8 x 35.5 x 20.4 (length x width x height).

## Learning Material Preparation

Prior to start learning to control the actuators and acquire data from the sensors on Hibiscus Sense using Arduino programming tool and language, we have to make sure all learning material is ready, as below:
1. Hibiscus Sense and a USB cable Type-A to Type-C _(suppose your computer only have Type-C USB port, you can also use USB cable Type-C to Type-C)_. If you don't have one, you are always welcome to purchase it from [Myduino](https://myduino.com/product/myd-036/)
2. A computer with Arduino IDE installed, if you don't have it please download it from here: [Windows](https://downloads.arduino.cc/arduino-1.8.13-windows.exe) / Linux [32-bit](https://downloads.arduino.cc/arduino-1.8.13-linux32.tar.xz), [64-bit](https://downloads.arduino.cc/arduino-1.8.13-linux64.tar.xz), [ARM 32-bits](https://downloads.arduino.cc/arduino-1.8.13-linuxarm.tar.xz) [ARM 64-bits](https://downloads.arduino.cc/arduino-1.8.13-linuxaarch64.tar.xz) / [Mac OSX](https://downloads.arduino.cc/arduino-1.8.13-macosx.zip) and install it on your computer.
3. [Arduino-ESP32](https://github.com/espressif/arduino-esp32) hardware library installed. Below is screenshot, showing the `Arduino IDE Boards Manager` (Arduino IDE Menu: **_Tools > Board:"_________" > Boards Manager..._**) which already have esp32 hardware library `INSTALLED`. If you don't have it, please follow this [instruction](https://github.com/espressif/arduino-esp32/blob/master/docs/arduino-ide/boards_manager.md) to install it.
<p align="center"><img src="https://github.com/myinvent/hibiscus-sense/raw/main/references/arduino-ide-hardware-library-esp32.png" width="600"></a></p>

## Interfacing Hibiscus to Computer's USB Port

Connect the USB cable Type-C to Hibiscus Sense and Type-A to our computer. Hibiscus Sense comes with preset program to test on-board actuators and sensors, should be by now we'll see the buzzer is buzzing, the RGB LED changing colors, the blue LED blinking and the reading of sensors at Serial Monitor (we have to open the Arduino IDE Serial Monitor to see the data). Suppose, you didn't see any reaction on the board you can contact Mr. Ariffin via [WhatsApp](https://api.whatsapp.com/send?phone=60177875232&text=Hi%20Mr.%20Ariffin,%20please%20help.%20My%20Hibiscus%20Sense,%20seems%20not%20working%20for%20the%20first%20time.) for help.

<p align="center"><img src="https://github.com/myinvent/hibiscus-sense/raw/main/references/hibiscus-sense-first-time.gif" width="600"></a></p>

<p align="center"><img src="https://github.com/myinvent/hibiscus-sense/raw/main/references/hibiscus-sense-first-time-monitor.gif" width="600"></a></p>

## Tutorial 1: Control Blue LED on GPIO2

There is 1x blue LED labelled as LED on-board. The circuit of this LED is an active-low and connected to GPIO2 ESP32, this means we have to pull the GPIO2 to LOW state, in order to complete the circuit to the GND.

<p align="center"><img src="https://github.com/myinvent/hibiscus-sense/raw/main/references/schematic-exercise-one.png" width="600"></a></p>
 
Therefore in the sketch, we need to call LOW state in the digitalWrite function, to light ON the LED, while call HIGH state, to light OFF the LED.