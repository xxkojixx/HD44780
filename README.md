# C library for HD44780 LCD driver

**in process ...**

## HD44780 Description
The HD44780U dot-matrix liquid crystal display controller and driver LSI displays alphanumerics,
Japanese kana characters, and symbols. It can be configured to drive a dot-matrix liquid crystal display
under the control of a 4- or 8-bit microprocessor. Since all the functions such as display RAM, character
generator, and liquid crystal driver, required for driving a dot-matrix liquid crystal display are internally
provided on one chip, a minimal system can be interfaced with this controller/driver.

A single HD44780U can display up to one 8-character line or two 8-character lines.
The HD44780U has pin function compatibility with the HD44780S which allows the user to easily replace
an LCD-II with an HD44780U. The HD44780U character generator ROM is extended to generate 208 5 x
8 dot character fonts and 32 5 x 10 dot character fonts for a total of 240 different character fonts.

The low power supply (2.7V to 5.5V) of the HD44780U is suitable for any portable battery-driven product
requiring low power dissipation. [HD44780 Datasheet](https://www.sparkfun.com/datasheets/LCD/HD44780.pdf)

## Features

- 5 x 8 and 5 x 10 dot matrix possible
- Low power operation support 
  - 2.7 to 5.5V
- Wide range of liquid crystal display driver power 
  - 3.0 to 11V
- Liquid crystal drive waveform 
  - A (One line frequency AC waveform)
- Correspond to high speed MPU bus interface 
  - 2 MHz (when VCC = 5V)
- 4-bit or 8-bit MPU interface enabled
- 80 x 8-bit display RAM (80 characters max.)
- 9,920-bit character generator ROM for a total of 240 character fonts
  - 208 character fonts (5 x 8 dot)
  - 32 character fonts (5 x 10 dot)

## Library
Library supports 4-bit and 8-bit communication with HD44780 LCD driver. Detail description how to interface with MCU is in:
- [4-bit Operation](#4-bit-operation)
- [8-bit Operation](#8-bit-operation)

### 4-bit Operation

Initializing LCD Driver HD44780 according to Figure 24 in [HD44780 Datasheet](https://www.sparkfun.com/datasheets/LCD/HD44780.pdf).
 ```c
 -----------------------------  
 |         Power on          |
 -----------------------------
              |
 -----------------------------
 | Wait for more than 15 ms  |
 | after VCC rises to 4.5 V  |
 -----------------------------
              |
 -----------------------------
 |  RS R/W DB7 DB6 DB5 DB4   |
 |   0   0   0   0   1   1   |
 -----------------------------
               |
 -----------------------------
 | Wait for more than 4.1 ms |
 -----------------------------
               |
 -----------------------------
 |  RS R/W DB7 DB6 DB5 DB4   |
 |   0   0   0   0   1   1   |
 -----------------------------
              |
 -----------------------------
 | Wait for more than 0.1 ms |
 -----------------------------  
              |
 -----------------------------
 |  RS R/W DB7 DB6 DB5 DB4   |
 |   0   0   0   0   1   1   |
 -----------------------------
               |
 -----------------------------
 | Wait for more than 41 us  |
 -----------------------------
               |
 -----------------------------   // 4 bit operation
 |  RS R/W DB7 DB6 DB5 DB4   |
 |   0   0   0   0   1   0   |
 -----------------------------
               |
 -----------------------------
 | Wait for more than 41 us  |
 -----------------------------
               |
 -----------------------------   // Display off
 |  RS R/W DB7 DB6 DB5 DB4   |   // 
 |   0   0   0   0   0   0   |   // D - display: 0 - no, 1 - yes
 |   0   0   1   D   C   B   |   // C - cursor: 0 - no, 1 - yes
 -----------------------------   // B - blink cursor: 0 - no, 1 - yes
               |
-----------------------------
| Wait for more than 41 us  |
-----------------------------
              |
-----------------------------   // Display clear
|  RS R/W DB7 DB6 DB5 DB4   |   // 0x01
|   0   0   0   0   0   0   |
|   0   0   0   0   0   1   |
-----------------------------
              |
-----------------------------
| Wait for more than 41 us  |
-----------------------------  
              |
-----------------------------   // Entry mode set
|  RS R/W DB7 DB6 DB5 DB4   |   // 
|   0   0   0   0   0   0   |   // I/D - shift cursor  (1 - left, 0 - right)
|   0   0   0   1 I/D   S   |   // S - shift text: 1 - no, 0 - yes  
-----------------------------
              |
-----------------------------
| Wait for more than 41 us  |
-----------------------------   
```
### 8-bit Operation

# Links
[HD44780 Datasheet](https://www.sparkfun.com/datasheets/LCD/HD44780.pdf)
