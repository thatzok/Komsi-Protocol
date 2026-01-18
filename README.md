# Komsi-Protocol

This protocol was inspired by the program "KOMSI" ("Kommunikationsschnittstelle für OMSI" which translates into "communication interface for OMSI").

It is used so that information (lamp status, door status, speed, etc.) can be transmitted from a bus simulator program (e.g. TheBus, OMSI 2) to e.g. a bus dashboard (usually based on Arduino or ESP32 CPUs).

How key presses and switch usage get from the dashboard to the bus simulator is not part of the KOMSI protocol. There are already established solutions for this. For example, an Arduino Leonardo or ESP32-S3 with their "HID" modules can register with a Windows PC as a game controller.

The original KOMSI program was only for the OMSI (and OMSI 2) simulator, but this KOMSI protocol tries to be interoperable, so that, for example, an Arduino-based bus dashboard that works with the KOMSI protocol works with both OMSI 2 and TheBus (and possibly other bus simulators in the future).

The text and line-based format also makes debugging easier. You can simply connect a terminal program (e.g. the Arduino IDE) to the USB port and send commands to the bus dashboard.

When assigning the command codes, an attempt was made to adopt the original assignment of the KOMSI program at the time. However, there are clear differences in the transmission of values ​​that are standardized in the KOMSI protocol, while in the original KOMSI program these depended individually on the respective dashboard. 
Example: "y50" in the Komsi protocol means that the speed "50" (km/h) should be displayed. In the original program, however, "50" was a servo value, and the speed displayed depends on the dashboard. And the "50" could mean 100 km/h, 30 km/h or something completely different, depending on how it was set in the dashboard. That was probably so that the Arduino code was as simple as possible, because the hardware was not yet as powerful as it is today.

The current status represents an interoperable basis that is already in practical use. However, there is no claim that all values ​​and special cases have already been taken into account. And the topic of "IBIS" in particular has so far been completely ignored.

---
Shield: [![CC BY-SA 4.0][cc-by-sa-shield]][cc-by-sa]

This work is licensed under a
[Creative Commons Attribution-ShareAlike 4.0 International License][cc-by-sa].

[![CC BY-SA 4.0][cc-by-sa-image]][cc-by-sa]

[cc-by-sa]: http://creativecommons.org/licenses/by-sa/4.0/
[cc-by-sa-image]: https://licensebuttons.net/l/by-sa/4.0/88x31.png
[cc-by-sa-shield]: https://img.shields.io/badge/License-CC%20BY--SA%204.0-lightgrey.svg

