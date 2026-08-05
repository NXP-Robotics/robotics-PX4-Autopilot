# NXP MR-TROPIC Flight Controller

TODO: clarify MR-TROPIC vs MR-VMU-TROPIC name

<Badge type="tip" text="PX4 v1.17" />

:::warning
PX4 does not manufacture this (or any) autopilot.
Contact the [manufacturer](https://www.nxp.com) for hardware support (https://community.nxp.com/) or compliance issues.
:::

The _MR-TROPIC_ reference design is based on the [Pixhawk<sup>&reg;</sup> FMUv6X-RT open standard](https://github.com/pixhawk/Pixhawk-Standards/blob/master/DS-020%20Pixhawk%20Autopilot%20v6X-RT%20Standard.pdf), the latest update to the successful family of Pixhawk<sup>&reg;</sup> flight controllers.

This is NXP's open source _reference design_ for using FMUv6X-RT, and was designed and made in collaboration with industry partners<sup>&reg;</sup>, NXP's mobile robotics team and the PX4 team.
As a reference/evaluation design, it is intended to be replicated, modified or integrated in production volume by others.
It has already gone through all FCC/CE ROHS REACH UKCA, EMI/RFI ESD certifications and is available globally.

TODO: add image

Besides the standard interfaces, the carrier board offers 100Base-T1 (two-wire) automotive Ethernet.
It also removes the IO processor to enable 8 PWM ports, all of them providing DShot capability.

This board takes advantage of multiple Pixhawk​​® open standards, such as the [Pixhawk<sup>&reg;</sup> FMUv6X-RT open standard](https://github.com/pixhawk/Pixhawk-Standards/blob/master/DS-020%20Pixhawk%20Autopilot%20v6X-RT%20Standard.pdf), [Autopilot Bus Standard](https://github.com/pixhawk/Pixhawk-Standards/blob/master/DS-010%20Pixhawk%20Autopilot%20Bus%20Standard.pdf), and [Connector Standard](https://github.com/pixhawk/Pixhawk-Standards/blob/master/DS-009%20Pixhawk%20Connector%20Standard.pdf).
Equipped with a high performance NXP i.MX RT1064 processor, modular design, temperature-controlled IMU board, isolated sensor domains, MR-TROPIC delivers incredible performance, reliability, and flexibility.

:::tip
This autopilot is [supported](../flight_controller/autopilot_pixhawk_standard.md) by the PX4 maintenance and test teams.
:::

## Introduction

Inside the MR-TROPIC, you can find an NXP i.MX RT1064, paired with sensor technology from Bosch® and InvenSense®, giving you flexibility and reliability for controlling any autonomous vehicle, suitable for both academic and commercial applications.

The Pixhawk® 6X-RT's i.MX RT1064 Crossover MCU contains an Arm® Cortex®-M7 core running up to 600 MHz, has 1MB SRAM and 4 MB on-chip flash.
The PX4 Autopilot takes advantage of the increased processing power and RAM.
Thanks to this increased processing power, developers can be more productive and efficient with their development work, allowing for complex algorithms and models.

The FMUv6X-RT open standard includes high-performance, low-noise IMUs on board, designed for better stabilization.

External sensor bus has one chip select line and data-ready signals for additional sensors and payload with SPI-interface, and with an integrated NXP TJA1103 Ethernet PHY, high-speed communication with mission computers via Ethernet is now possible.

The MR-TROPIC reference design is perfect for developers at corporate research labs, startups, academics (research, professors, students), and commercial application that like to try out T1 (2 wire) automotive Ethernet.

Note that since it is a reference design, this _particular_ board is not produced in high volume.
Similar variants will be available from our licensees.

## Key Design Points

- High performance [NXP i.MX RT1064 600 MHz Crossover MCU](https://www.nxp.com/products/i.MX-RT1064) with Arm® Cortex® core
- Modular flight controller: separated IMU, FMU, and Base system connected by a 100-pin & a 50-pin Pixhawk® Autopilot Bus connector
- Redundancy: 2x IMU sensors on separate buses
- Newly designed vibration isolation system to filter out high frequency vibration and reduce noise to ensure accurate readings
- 100Base-T1 2-Wire Ethernet interface for high-speed mission computer integration
- IMUs are temperature-controlled by onboard heating resistors, allowing optimum working temperature of IMUs&#x20;

## Processors & Sensors

- FMU Processor: NXP i.MX RT1064
  - 32 Bit Arm Cortex-M7, 600MHz
  - On-chip 4MB flash
  - 1 MB on-chip SRAM - up to 512 KB configurable as tightly coupled memory (TCM)

- On-board sensors:
  - Accel/Gyro: TDK InvenSense ICM-45686
  - Accel/Gyro: Bosch BMI088
  - Mag: Bosch BMM350
  - Pressure Sensor: Bosch BMP390

## Electrical Data

- Voltage Ratings:
  - Max input voltage: 5.5V
  - USB Power Input: 5V
  - Servo Rail Input: TODO

- Current Ratings: TODO

## Mechanical Data (dimensions & weight)

- Dimensions:
  - Standard Baseboard: 46 x 45 x 1.57mm
- Weight:
  - Standard Baseboard: TODO

## Assembly/Setup

Wiring is similar to the [Holybro Pixhawk 6X](../flight_controller/pixhawk6x.md#connections) and other boards that follow the [Pixhawk Connector Standard](https://github.com/pixhawk/Pixhawk-Standards/blob/master/DS-009%20Pixhawk%20Connector%20Standard.pdf).

## Connections

_MR-VMU-TROPIC_ connectors (following [Pixhawk Connector Standard](https://github.com/pixhawk/Pixhawk-Standards/blob/master/DS-009%20Pixhawk%20Connector%20Standard.pdf))
TODO images

![MR-VMU-TROPIC Top Image](../../assets/flight_controller/nxp_mr-vmu-tropic/mr-vmu-tropic_top.jpg)
![MR-VMU-TROPIC Front Image](../../assets/flight_controller/nxp_mr-vmu-tropic/mr-vmu-tropic_front.jpg)
![MR-VMU-TROPIC Leftside Image](../../assets/flight_controller/nxp_mr-vmu-tropic/mr-vmu-tropic_top.jpg)
![MR-VMU-TROPIC Rightside Image](../../assets/flight_controller/nxp_mr-vmu-tropic/mr-vmu-tropic_top.jpg)

The NXP reference board design production version units have a slightly different connector set than what has tradionally been included in the standard V6X design and also the Holybro V6X-RT units.

The key differentiators are:
-  No separate IO processor required. All PWMs including redundant coming from RT1064

* CAN port
* 100BaseT1 two wire Ethernet

### Top side interface

* USB-C interface
* PWM_A and PWM_B

TODO image

### Back side interface

* RC receiver connector
* Primary GPS port
* Auxiliary UART connector
* Telemetry Port 1
* Telemetry Port 2
* Debug interface compliant to Pixhawk-DEBUG-FULL standard (aka DCD-F), including SWD and Console access.
* T1-ETH: 100BaseT1 Two wire 100MBPS Ethernet 
* CAN: Dual CAN-FD interfaces employing CAN-SIC (Signal Improvement) CAN phys
* OSD: SPI expansion connector
* Power input

TODO image

### Debugger and serial console connection
TODO image

### Indicator LEDs
TODO image

## Pinouts

### Top view TODO

![MR-VMU-TROPIC Top Image](../../assets/flight_controller/nxp_mr-vmu-tropic/mr-vmu-tropic_top.jpg)

### Back view TODO

![MR-VMU-TROPIC Top Image](../../assets/flight_controller/nxp_mr-vmu-tropic/mr-vmu-tropic_top.jpg)

### Left side view TODO

![MR-VMU-TROPIC Top Image](../../assets/flight_controller/nxp_mr-vmu-tropic/mr-vmu-tropic_top.jpg)

### Right side view TODO

![MR-VMU-TROPIC Top Image](../../assets/flight_controller/nxp_mr-vmu-tropic/mr-vmu-tropic_top.jpg)


## Building Firmware
> Most users will not need to build this firmware!
It is pre-built and automatically installed by _QGroundControl_ when appropriate hardware is connected.


To [build PX4](https://docs.px4.io/main/en/dev_setup/building_px4) for this target:

```sh
make nxp_mr-tropic_default
```

## Debug Port

The [PX4 System Console](https://docs.px4.io/main/en/debug/system_console) and [SWD interface](https://docs.px4.io/main/en/debug/swd_debug) run on the FMU Debug port.

The pinouts and connector comply with the [Pixhawk Debug Full](https://docs.px4.io/main/en/debug/swd_debug#pixhawk-debug-full) interface defined in the [Pixhawk Connector Standard](https://github.com/pixhawk/Pixhawk-Standards/blob/master/DS-009%20Pixhawk%20Connector%20Standard.pdf) interface (J3 JST SM10B connector).

| Pin      | Signal           | Volt  |
| -------- | ---------------- | ----- |
| 1 (red)  | `Vtref`          | +3.3V |
| 2 (blk)  | Console TX (OUT) | +3.3V |
| 3 (blk)  | Console RX (IN)  | +3.3V |
| 4 (blk)  | `SWDIO`          | +3.3V |
| 5 (blk)  | `SWCLK`          | +3.3V |
| 6 (blk)  | `SWO`            | +3.3V |
| 7 (blk)  | NC               |   -   |
| 8 (blk)  | NC               |   -   |
| 9 (blk)  | nRST             | +3.3V |
| 10 (blk) | `GND`            | GND   |

For information about using this port see:

- [SWD Debug Port](../debug/swd_debug.md)
- [PX4 System Console](../debug/system_console.md)


## Interfaces

- 8 PWM servo outputs, all 8 with DShot
- Dedicated R/C input for CRSF / ELRS
- 3 general purpose serial ports:
  - 3 with full flow control
- 1 GPS port
  - 1 full GPS plus Safety Switch Port
- 1 I2C port
- 1 Ethernet port
  - Transformerless Applications
  - 100Mbps
- 1 SPI bus (OSD)
  - 1 chip select line
  - 1 data-ready line
  - 1 reset line
- 1 CAN Bus for CAN peripheral
  - Termination resistor on-board (120 ohm)
- 1 Power input port with SMBus
- 1 Debug port

- Other Characteristics:
  - Operating & storage temperature: {TODO}°c
