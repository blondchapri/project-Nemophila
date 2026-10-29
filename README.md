# project-Nemophila
HID system used for displaying ,acquisition and processing of vehicle data  designed for  a E-BAJA atv in accordance with SAE India rulebook 2027 
# Overview
This is a 2 board design; I have split the boards to save space and cost.\
### Board 1 utilizes: 
+ an Arduino Uno Q for all the acquisition and processing of vehicle data 
+ a MP2338GTL-Z SMPS used to power the whole system, it takes in a 12V battery and steps it down to 5v 
+ a TJA1042T_3_CM_118 CAN transceiver to collect data from all the other systems from the buggy 
+  Arduino Mega 3.2’’ TFT hat/ shield used to display relevant and specialized data and fault messages using AI models running on the Uno-Q
### Board 2 utilizes:
+ 2x HT16K33 used to drive the segment displays; it receives its 12c signal from Board 1 
+ 9x .8 inch 16 segments, one for battery SOC, one for voltage, one for battery temperature 
+ Board 2 gets its power from Board 1 

# Board 1
<img width="1391" height="1253" alt="image" src="https://github.com/user-attachments/assets/e7a27246-7314-496c-a477-4974cb6c9ca6" />


This is the main board of this system where all the control and computation is done\
It’s a 4 layer board, with the 2 outer layers being primarily for signals with a ground pour, layer 2 for ground, and layer 3 for +5V

<img width="847" height="451" alt="image" src="https://github.com/user-attachments/assets/5729d257-0aa8-4794-8b5a-ab0df5c5cd5b" />


## Uno-Q
<img width="759" height="605" alt="image" src="https://github.com/user-attachments/assets/29ea50b9-1bd5-4679-b9aa-95e6d9bf1198" />


I won't go into detail about it, but to know more about this banger of a single-board computer, you should [read its documentation](https://docs.arduino.cc/hardware/uno-q/#features)\
Basically, it has 2 processors, Qualcomm Dragonwing QRB2210 based on  Arm Cortex-A53 of which it has 4 cores. This runs our AI model [it can also ''play'' games](https://youtu.be/YrrqF2y-dlM?si=kdVxpX9fKiZ1ygUE) 
and the second chip is the STM32U585 microcontroller based on Arm Cortex-M33, which is used for all our embedded shenanigans

The Uno Q has the 120 highspeed pins on the underside 60 per processor and the rest in the standard Uno config on top, which are primarily STM32U585 GPIO. We used pin headers for the underside connectors and headers with jumper wires for the top GPIO pins. Most of our needs are met by the STM32 used to drive the 3.2 inch TFT and the 9 segment displays stm32 is also used for the CAN bus communication 
<img width="1619" height="704" alt="image" src="https://github.com/user-attachments/assets/5b944612-adaf-4900-a591-2f79399dffa2" />

<img width="897" height="915" alt="image" src="https://github.com/user-attachments/assets/ffc29f47-5db5-416c-9ebc-a142f07fdaf2" />


Highlighted parts are part of the UNO-Q subsystem.

## MP2338GTL-Z 
I mean it’s a power supply\
Why I chose it : [[insert AI’s answer]](https://github.com/blondchapri/project-Nemophila/blob/main/ai)\
it takes the 12v battery input from the xt60 and steps it down to +5V
<img width="2005" height="1061" alt="image" src="https://github.com/user-attachments/assets/b9f8aefb-c995-4c01-b84c-47d05528c91c" />

<img width="1834" height="1210" alt="image" src="https://github.com/user-attachments/assets/de3ba0f0-fd50-47cd-8148-8684ad82f6db" />
)

## TJA1042T_3_CM_118
CAN transceiver works with both 3V3 and 5v logic, cheap and easy to find online and in offline shops!!!!! Yes please

<img width="1996" height="798" alt="image" src="https://github.com/user-attachments/assets/d8ec7281-312f-431f-bbbb-da244a86cefd" />


<img width="1950" height="936" alt="image" src="https://github.com/user-attachments/assets/ef089524-8b0a-4049-9ebd-b84a750f23a9" />



## Arduino Mega 3.2’’ TFT hat
why specifically this one?\
Well, we needed a display I had this lying around for an unrelated personal project, and my stingy team said GIVE IT HERE. And that is why this one.\
You can learn about this display by reading the uploaded PDFs or [the LCDWIKI article](https://www.lcdwiki.com/3.2inch_Arduino_Display-Mega2560)

<img width="500" height="285" alt="image" src="https://github.com/user-attachments/assets/b515b0a4-6179-411f-8a4e-5d5d5d9e137d" />




# Board 2

This is a 2 layer board only used for the segment display, which is why I thought not to waste money by using a 4 layer board  
It gets its power and I2C signal from board 1
HT16K33 works on 5V logic, so it needs a logic level shifter to work with UNO-Q which is present on Board 1

<img width="758" height="369" alt="image" src="https://github.com/user-attachments/assets/1a80fe17-577d-4005-815f-6a0f3cd71183" />

<img width="1392" height="1254" alt="image" src="https://github.com/user-attachments/assets/95f0da3f-28d0-47d7-9249-d9e883ed6c18" />

<img width="1867" height="1014" alt="image" src="https://github.com/user-attachments/assets/dfd3ea09-a6ba-44d9-8195-145c6744d394" />

<img width="1187" height="1201" alt="image" src="https://github.com/user-attachments/assets/6a57228a-7c6e-4d81-802e-94e448f5a61b" />



## why the name
I recently got into illustrated flower artworks and decided that all my projects and work will be named after cool flowers.

Why Nemophila? I absolutely adore this flower and its blue hue. I had the honour of witnessing its beauty in real life last year (2025) at Anime India Mumbai, where a Frieren cosplayer had made a tiara of them. Ever since then, their etherealness is stuck in my head. Also Rei Ayanami's hair colour is similar and gives the same feeling, and I am a big time EVA fan 
<img width="2592" height="1944" alt="image" src="https://github.com/user-attachments/assets/2ffb9890-8d1c-435c-b716-f9487add0e32" />

### <a href="https://github.com/blondchapri/project-Gulmohar">Project Gulmohar</a> © 2026 by <a href="https://github.com/blondchapri">shlok shukla</a> is licensed under <a href="https://creativecommons.org/licenses/by-nc-sa/4.0/">Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International</a>
# <img src="https://mirrors.creativecommons.org/presskit/icons/cc.svg" alt="" style="max-width: 1em;max-height:1em;margin-left: .2em;"><img src="https://mirrors.creativecommons.org/presskit/icons/by.svg" alt="" style="max-width: 1em;max-height:1em;margin-left: .2em;"><img src="https://mirrors.creativecommons.org/presskit/icons/nc.svg" alt="" style="max-width: 1em;max-height:1em;margin-left: .2em;"><img src="https://mirrors.creativecommons.org/presskit/icons/sa.svg" alt="" style="max-width: 1em;max-height:1em;margin-left: .2em;">
