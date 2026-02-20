# [cite_start]Schneckomat: Automated Snail Habitat Controller 

[cite_start]The **Schneckomat** is an Arduino-based environmental control system designed to regulate temperature and lighting for snail terrariums[cite: 1, 4, 35]. [cite_start]It features a dynamic day/night cycle, automated heating, and a custom OLED interface with a traveling snail animation[cite: 4, 5, 109].

---

## ### Hardware Configuration

The system utilizes the following pin assignments and protocols:

| Component | Pin / Interface | Description |
| :--- | :--- | :--- |
| **Relay (Heat)** | [cite_start]Pin 3  | Controls the heating element. |
| **Triac Dimmer** | [cite_start]Pin 9  | Controls light intensity via PWM/Phase cutting. |
| **Select Button** | [cite_start]Pin 6  | Menu navigation and confirmation. |
| **Up Button** | [cite_start]Pin 5 [cite: 2] | Increments values/Scrolls up. |
| **Down Button** | [cite_start]Pin 4  | Decrements values/Scrolls down. |
| **OLED Display** | [cite_start]I2C (SSD1306)  | 128x64 pixels for UI feedback. |
| **Sensor (DHT20)**| [cite_start]I2C  | Measures ambient temperature and humidity. |
| **RTC (DS3231)** | [cite_start]I2C  | Keeps real-time for day/night scheduling. |

---

## ### Environmental Logic

### [cite_start]Temperature Control [cite: 35]
The controller maintains specific temperature ranges depending on the time of day:
* [cite_start]**Daytime (08:00 - 22:00)**: Aims for a range between **24.0°C** and **27.0°C**[cite: 4, 5, 53, 54].
* [cite_start]**Nighttime (22:00 - 08:00)**: Aims for a range between **20.0°C** and **23.0°C**[cite: 4, 53, 54].
* [cite_start]**Hysteresis**: A buffer of **0.5°C** is applied to prevent rapid relay clicking[cite: 5, 55, 56].

### [cite_start]Lighting [cite: 35]
* [cite_start]**Automatic Cycle**: Lighting levels adjust automatically throughout the day to simulate natural progression[cite: 66, 67].
* [cite_start]**Manual Override**: Users can manually toggle the light or set a specific "Light %" through the menu[cite: 75, 76, 77].
* [cite_start]**Dimming Range**: Light intensity is mapped from a baseline value to a maximum of 100%[cite: 64, 92].

---

## ### User Interface

### Main Screen
[cite_start]Displays current humidity, time, and temperature[cite: 38, 40]. [cite_start]A snail icon travels across the screen; when it reaches the edge, it resets its position to simulate continuous movement[cite: 70, 71, 109].

### [cite_start]Menu Options [cite: 31]
1.  [cite_start]**Light On/Off**: Toggles manual light mode[cite: 75].
2.  [cite_start]**Light %**: Adjusts the maximum brightness of the lamp[cite: 77, 91, 101].
3.  **Temp. [cite_start]Day**: Configures Max and Min thresholds for daytime[cite: 78, 82, 83].
4.  **Temp. [cite_start]Night**: Configures Max and Min thresholds for nighttime[cite: 79, 84, 85].
5.  [cite_start]**Back**: Returns to the main animation screen[cite: 80].

> [cite_start]**Note**: If no buttons are pressed for 60 seconds (60,000ms), the screen automatically reverts to the Main Screen[cite: 87].

---

## ### Technical Implementation Details

* [cite_start]**EEPROM Persistence**: All user-defined temperature and light settings are saved to EEPROM[cite: 1, 32]. [cite_start]On startup, the system checks for an initialization flag ('T') at address 17 to restore your settings[cite: 32, 33, 34].
* [cite_start]**DST Adjustment**: Includes a `summertime` function to automatically adjust for Daylight Saving Time[cite: 122, 124, 125].
* [cite_start]**Non-Blocking Logic**: Uses `millis()` for time calculations and button debouncing to ensure the snail animation remains smooth[cite: 121].
