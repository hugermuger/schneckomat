# Schneckomat: Automated Snail Habitat Controller

The **Schneckomat** is an Arduino-based environmental control system designed to regulate temperature and lighting for snail terrariums. It features a dynamic day/night cycle, automated heating, and a custom OLED interface with a traveling snail animation.

---

## ### Hardware Configuration

The system utilizes the following pin assignments and protocols:

| Component | Pin / Interface | Description |
| :--- | :--- | :--- |
| **Relay (Heat)** | Pin 3 | Controls the heating element. |
| **Triac Dimmer** | Pin 9 | Controls light intensity via PWM/Phase cutting. |
| **Select Button** | Pin 6 | Menu navigation and confirmation. |
| **Up Button** | Pin 5 | Increments values/Scrolls up. |
| **Down Button** | Pin 4 | Decrements values/Scrolls down. |
| **OLED Display** | I2C (SSD1306) | 128x64 pixels for UI feedback. |
| **Sensor (DHT20)**| I2C | Measures ambient temperature and humidity. |
| **RTC (DS3231)** | I2C | Keeps real-time for day/night scheduling. |



---

## ### Environmental Logic

### Temperature Control
The controller maintains specific temperature ranges depending on the time of day:
* **Daytime (08:00 - 22:00)**: Aims for a range between **24.0°C** and **27.0°C**.
* **Nighttime (22:00 - 08:00)**: Aims for a range between **20.0°C** and **23.0°C**.
* **Hysteresis**: A buffer of **0.5°C** is applied to prevent the relay from toggling too frequently.

### Lighting
* **Automatic Cycle**: Lighting levels adjust automatically throughout the day to simulate sunrise and sunset.
* **Manual Override**: Users can manually toggle the light or set a specific "Light %" through the menu.
* **Dimming Range**: Light intensity is mapped from a baseline value to a maximum of 100%.

---

## ### User Interface

### Main Screen
Displays current humidity, time, and temperature. A snail icon travels across the screen; when it reaches the edge, it resets its position to simulate continuous movement.

### Menu Options
1.  **Light On/Off**: Toggles manual light mode.
2.  **Light %**: Adjusts the maximum brightness of the lamp.
3.  **Temp. Day**: Configures Max and Min thresholds for daytime.
4.  **Temp. Night**: Configures Max and Min thresholds for nighttime.
5.  **Back**: Returns to the main animation screen.

> **Note**: If no buttons are pressed for 60 seconds, the screen automatically reverts to the Main Screen.

---

## ### Technical Implementation Details

* **EEPROM Persistence**: All user-defined temperature and light settings are saved to EEPROM. On startup, the system restores your settings automatically.
* **DST Adjustment**: Includes a built-in logic to automatically adjust for Daylight Saving Time.
* **Non-Blocking Logic**: Uses `millis()` for time calculations and button debouncing to ensure the snail animation remains smooth.
