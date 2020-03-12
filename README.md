# STM32G031J6M6 Breakout Board
![](https://github.com/nathancharlesjones/STM32G031J6M6-Breakout-Boards/blob/master/STM32G031J6M6_PCB.png)

# How to order
1. Download or clone this repository.
2. Follow [these instructions for ordering an assembled PCB from JLCPCB or MakerFabs](https://github.com/nathancharlesjones/Embedded-for-Everyone/wiki/3.-Building-a-circuit-on-a-PCB-and-connecting-it-to-the-rest-of-the-embedded-device#ordering-an-assembled-pcb).

This board was also designed with large-enough dimensions to be manufactured by hand using a PCB mill or other manual technique. If the method you use doesn't through-plate the vias, don't forget to connect them each yourself.

# STM32G031J6M6 specifications
|Processor|Core Size|Speed|Connectivity|Peripherals|I/O|Program memory size|RAM size|Data converters|
|---|---|---|---|---|---|---|---|---|
|ARM Cortex-M0+|32-bit|64 MHz|I2C, IrDA, LINbus, SPI, UART/USART|Brown-out Detect/Reset, DMA, I2S, POR, PWM, WDT|6<sup>1</sup>|32 kB|8 kB|ADC: 8x 12-bit|

Notes:
1. Of the 6 GPIO this MCU supposedly has, one is used for reset and two are used for the SWD interface, meaning this MCU, realistically, only has 3 GPIO.

# Schematic
![](https://github.com/nathancharlesjones/STM32G031J6M6-Breakout-Boards/blob/master/STM32G031J6M6_Schematic.png)

The schematic for this breakout board includes 5 modules or sections:
1. MCU
   - The MCU itself and the 0.1" pin header to which most of the MCU pins are connected (U1 and J1).
2. Power 
   - Power regulator, power filtering capacitors, and an LED indicator (IC1, D1, D2, C2, C3, C4, PWR LED, and R1).
   - Only C2 and C3 are technically required for MCU operation. If you decide to only include those two components, don't forget to bridge the pads of D2.
   - If IC1 is used, D1 and D2 are strongly recommended, though not technically required. D1 and D2 allow for the MCU to be powered from both the VIN_1.7-3.6V and VIN_5-30V pins at the same time without them damaging each other.
3. Reset
   - The reset button and smoothing capacitor (S1 and C1).
4. User LED
   - LED, current-limiting resistor, and option jumper (USER LED, R2, and J3)
   - J3 is used to optionally remove the LED from the circuit, should you wish to not have the LED connected to its GPIO.
   - To remove LED2 from the circuit, cut the trace between the terminals of J3 on BOTTOM of the PCB (where its marked on the silkscreen).
   - To reinsert USER LED, place a pin header and jumper in J3. The jumper now controls whether USER LED is included in the circuit or not.
5. J-Link connector (J2)

The cost is approximately $3.30 on JLCPCB (in quantities of 10).

# PCB Silkscreen Text
> - V_IN, 1.7-3.6V: Connected thru D2 to V_DD; MCU damage may occur if >4V applied to this pin.
> - V_IN, 5-30V: Connected to input of IC1
> - Max GPIO current, single pin: 15 mA
> - Max GPIO current, all pins: 80 mA
> - USER LED connected to C14 (pin 1). Cut trace btwn J3 pins on BOTTOM of PCB to remove LED from circuit (in-stall jumper on TOP to reinsert LED)
> ------------------------------
> - U1: STM32G031J6M6 / SOIC8
> - IC1: 1.7-3.6V regulator / SOT89-3 (ex: HT7533-1 from Holtek Semicon)
> - J1, 1st 4 terminals (in box): ST-Link connection points
> - J2: J-Link connector (ex: HPH2-A-10-UA-SMT from Adam Tech or 3221-10-0300-00 from CNC Tech)
> - C1, C3: 100nF / 1206  | C2: 4.7uF / 1206
> - C4: 10 uF / 1206      | R1, R2: 1206 (~100ohms)
> - S1: SPST-NO / 5.1mmx5.1mm (ex: TS-1187A-B-A-B from XKB Enterprises)
> - PWR/USER LED: 0805
> - D1, D2: Shottky diode | DO-214AC
> - FMI: github.com/nathancharlesjones/Embedded-for-Everyone/wiki

# References
- [STM32G031J6 product page](https://www.st.com/content/st_com/en/products/microcontrollers-microprocessors/stm32-32-bit-arm-cortex-mcus/stm32-mainstream-mcus/stm32g0-series/stm32g0x1/stm32g031j6.html)
- [AN5096, Getting started with STM32G0 series hardware development](https://www.st.com/resource/en/application_note/dm00443870.pdf)
- [DS12992](https://www.st.com/resource/en/datasheet/stm32g031j6.pdf), STM32G031J6M6 datasheet
- [RM0444](https://www.st.com/resource/en/reference_manual/dm00371828.pdf), STM32G031J6M6 reference manual
