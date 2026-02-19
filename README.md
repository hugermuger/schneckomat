\# 🐚 Snail Enclosure Controller Pro



An Arduino-based environment manager featuring AC light dimming, heat regulation, and a custom icon-driven menu system.



\## 🌟 Features

\- Dual-Climate Control Separate target temperatures for Day and Night with a 0.5°C buffer.

\- Animated Interface Real-time snail animation that moves across the screen.

\- EEPROM Memory Saves your settings automatically so they aren't lost during power outages.



\## 🔌 Pin Map

&nbsp;Component       Arduino Pin  Connection Type 

----------------------------------------------

&nbsp;OLED Display		      I2C             

&nbsp;RTC (Clock)     	      I2C             

&nbsp;DHT20 Sensor   	      I2C             

&nbsp;Triac Dimmer    D9           PWM  AC Phase  

&nbsp;Heater Relay    D3           Digital Output  

&nbsp;Select Button   D6           Input Pullup    

&nbsp;Up Button       D5           Input Pullup    

&nbsp;Down Button     D4           Input Pullup    



\## 🛠 Setup

1\. Open the `.ino` file in the Arduino IDE.

2\. Install the following libraries `U8g2`, `DHT20`, `RTClib`, and `TriacDimmer`.

3\. Upload to your Arduino Uno.

