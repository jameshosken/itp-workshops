


## Microcontrollers

## Overview

Now that we have some mad electronic skillz, what can we do with them? We can use them to assemble, hack, and prototype all sorts of different circuits. But they'll likely be dumb circuits: press a button and an LED turns on, or turn a knob to change the speed of a fan. 

A microcontroller is a way to automate that control, add an electronic *brain* to your circuit to turn those knobs and switches for you.

### What Is A Microcontroller? 
An electronic chip that takes inputs and turns them into outputs. 

### ITP's Flavour of Electronics
In general what we do here at ITP is take some bizarre input, do something funky to it, and then there's some bizarre output. The electronics above are helpful in building the inputs and outputs (in our basic case the button and the LED), but the core of these input > process > output systems is a microcontroller.

### Types of controllers
There are many different types of microcontrollers, but the folks over at Arduino have created a system around a specific one that makes programming and using it relatively beginner friendly. The black box on your Arduino is the microcontroller, the rest is the system around it. 


### Why Not Use Computers?
In general, microcontrollers are:
- **Dumb** (can't do intense processing, unlike PCs)
- **Small and cheap** (unlike PCs)
- **Are embedded, in that they only need to do one set of tasks** (unlike PCs)

---

## Arduino

So far we've only used the Arduino as a power source, we have not accessed its usefulness as a *brain*. To use it as a brain we must upload a program to it, so it knows what to do! How do we do that?

### Arduino Rundown

- **Power:** 5V board
	- USB or 7-15V 
	- 40mA *per pin*, 500 mA *max* | **Don't fry your board!**
- **Pins:** Digital vs Analog.
	- Digital 	(Read or Write 5V)
	- Analog	(Read 0V - 5V, Write 5V)
	- **PWM (~):** A way to fake analog;

#### A Note On Power
The Arduino max rating is 40mA per pin, so what if you want to control a motor that draws 200mA? or 500mA? Controlling high current loads is outside the scope of this workshop, but there are many ways to do it. Here are some of the common ways if you'd like to delve deeper:

- **Transistors,** which sort of act as electronic switches. Give a transistor a small current and it turns on a high current circuit.
- **Motor Drivers.** Essentially a motor driver is a fancy switch that controls your motor. Instead of manually controlling the switch, you plug it into your Arduino. Among other things they can be:
 	- super cheap [single chips](https://www.pololu.com/product/24), 
 	- [Arduino-compatible shields](https://www.adafruit.com/product/1438?gclid=EAIaIQobChMI27L7ycXn4gIVWuDICh0fDQ0NEAQYASABEgLisvD_BwE),
 	- [expensive and robust circuits](https://motorsandcontrol.com/bodine-electric-0786-012-0-14-vdc-167-hp-chassis-dc-drive/?utm_source=google_shopping&keyword=&gclid=EAIaIQobChMIupSc38Tn4gIVjlcNCh2cUAI-EAQYASABEgIPFPD_BwE).




### Setting Things Up
1. Install [Arduino](https://www.arduino.cc/en/Main/Software)
	- You can use the Web Editor but it requires a plugin and the setup time is just as much as the standalone application setup time. I usually use the standalone application.
2. Plug in your Arduino.
4. Under **Tools > Board** select *Arduino/Genuino Uno*
5. Under **Tools > Port** select the port your Arduino is on\*
	- On a Windows with will look like *COMXX*
	- On a Mac, this will look like "/dev/tty.usbserial-XXXXXXXX"

#### Potential Frictions\*
If you don't see port listed, try this:

1. Since Arduino is open source, there are many derivations of the board. The genuine Arduino should register on your computer, but if you have a different board you may need to install drivers for that board.
2. Unplug and replug.


### Blinking an LED

1. Open up the app and click **File > Examples > 01Basics > Blink**
2. Connect **Pin 13** to the positive side of your LED circuit, and **GND Pin** to the ground.

---

## General Electronics Tinkering Guidelines

### Safety Tips for You
1. Always **wash your hands** afterwards. Electronics stuff is nasty.
2. Don't use AC power until [you know what you're doing](https://engineering.nyu.edu/academics/programs/electrical-engineering-ms). 

### Safety Tips for Your Stuff
1. Pay attention to the Datasheets. You will find all sorts of useful information about max current, min/max voltage. Knowing these will help you avoid turning your circuits into blue smoke. 
2. Avoid food or water around electronics. 
