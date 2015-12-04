# Worgbox
ESP8266 Controlled Grow Box with external web application for monitoring parameters, sensors data, change settings, etc.

## Introduction
Growbox named 'Worgbox'. What do I mean? 'Worg' and 'box'! 'Worg' in parallel universe sounds like 'Grow'. 
No need to explain you how we can travel there :]
Main idea I want to make a very compact and controlled box for growing something small in little area and possible stealthy.

>It's second version of controller. First version (repo [Worgbox-Proto](https://github.com/GrowBoxer/Worgbox-Proto)) based on Arduino + ESP8266 ESP-01.
>Works, with questions, repo still (and forever?) without code and other stuff. Migrating here.

## Features
- read sensors data
- controll day/night cicles
- etc

## Components

### Construction
- Material is 6mm laser cutted plywood
- External dimensions 260mm x 260mm x 470mm
- Internal dimensions for a plant 248 mmm x 170 mm x 360 mm

### Controller
- ESP8266 ESP-12

### Sensors
- DHT22 
- 2x DS18B20 (3x optional)

### Light
- 16x 3W full spectrum LEDs

### Fans
- 2x 12cm FANs (3x optional)

### Additional
- OLED 128x64 I2C display
- 2x DC SSR
- LED driver
- Precise clock module ds3231

## How It Works
Controller have 4 light modes: 24/0, 18/6 (default), 12/12 and 0/24 (hours of day/night). ON/OFF by SSR.
Default time when night starts: 18:00.
Default FANs speed: 90% when day, and 30% when night (range 30-95%). Regulated by PWM with SSR. At FAN SSR control PIN PWM frequency lower than standart(?).
Using http you can change this modes and parameters.
OLED Display show main parameter, current time also temperatures and humidity.
Controller connects to your WiFi AP, take IP by DHCP and starts web server. Http request answer is JSON (current parameters, sensors data, etc.).

## HTTP Commands
You can use this commands for change settings and receive sensors and other data without using web server.

Usual request looks like http://your.controller.ip.address/command/option/value

List of /command/option/value

- [/get/json](#) - return JSON string with all current system state data (sensors, light mode, time, etc.)
- [/set/light-mode/0](#) — set light mode to 24/0 (hours of day/night) (always day)
- [/set/light-mode/1](#) — set light mode to 18/6 
- [/set/light-mode/2](#) — set light mode to 12/12 
- [/set/light-mode/3](#) — set light mode to 0/24 (always night)
- [/set/fans-day-mode/90](#) — set fans speed to 90% of max when day (min 50% max 100%)
- [/set/fans-night-mode/30](#) — set fans speed to 30% of max when night (min 30% max 100%)
- [/set/night-starts/18](#) — set time when night starts

## Files

#### Construction

- PlywoodLaserCut.dwg — 2d scheme of each plywood sheet for laser cutting in DWG format (AutoCAD).
- Worgbox.max — 3d model of box in 3dsmax format;

#### Schematic

- wiring.xxx;
- pcblayout.xxx;

#### Code

- worgbox.ino+ — arduino ide for ESP8266 sketch;

#### Web

- index.php+ — scripts for monitoring and change parameters
- grabber.php — script for parse json and send data to thingspeak.com
- alerter.php - script for notificate by email when one of specified value over/less than normal

#### Examples

- data.json — example of data recieved from controller;
- data.csv — example of data sended to thingspeak;

### TO DO Files
- check DWG for actual changes
- need back door fan shift
- need solid plywood base for light compartment door

### TO DO Construction
- use bigger holles for wires (up to 5 mm diameter)
- separate high voltage and low voltage compartments;


### TO DO Hardware
- make PCB for complete product;
- setup temeprature sensor to the LED radiators;
- read white wire data from the fans (for RPM analyze);

### TO DO Software
- analyze fans RPM;

## TO DO HTTP Commands
- [/set/light-fans-day-mode/90](#)
- [/set/box-fans-day-mode/90](#)
- [/set/light-fans-night-mode/0](#)
- [/set/box-fans-night-mode/30](#)

### Ideas Components
- different SSR relays for PWM control light and box fans (different RPM)


### Ideas Construction
- transparent acrylic window for revision of main area
- one-point lock for main door (now have 4-point locks) — construction should be strong
- put screws deeper (into first plywood layer)
