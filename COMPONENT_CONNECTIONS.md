# Outback Edge v1.0 - Component Connections Documentation

## Overview

This document describes the component connections for the Outback Edge v1.0 hardware platform. The board uses a custom **OutbackEdge-M2e-Mod-Interface-v1.0** standard for the M.2 E-Key connector, which is designed for MCU-oriented expansion modules (not standard PC M.2 devices).

---

## Component List

| Reference | Description | Package/Type |
|-----------|-------------|--------------|
| U1 | Renesas R7FA6M5AH3CFB#AA0 ARM Cortex-M33 MCU | 144-pin LQFP |
| U2 | USB2514B USB 2.0 Hi-Speed Hub Controller | QFN-36 |
| J1 | USB Type-C Receptacle (USB 2.0, 16-pin) | USB_C_Receptacle_USB2.0_16P |
| J2 | M.2 Socket E-Key (75-pin) - OutbackEdge-M2e-Mod-Interface | OE_M.2_Socket_E |
| J3 | RJ45 Ethernet with LEDs, Shielded | RJ45_LED_Shielded |
| J4 | Micro SD Card Socket with Detection | Hirose DM3AT |
| J5 | USB 3.0 Type-A Stacked Connector | USB3_A_Stacked (dual port) |
| BT1 | Battery Cell (backup power) | Battery_Cell |
| SW1 | Push Button Switch | SW_Push |
| C1-C9 | Decoupling Capacitors (0.1uF) | Various SMD |
| R1 | Resistor | SMD |

---

## Signal Connections

### SDIO Bus (SD Card Interface)
Connects: **U1 (MCU)** ↔ **J4 (MicroSD)** ↔ **J2 (M.2 Socket)**

| Signal | MCU Pin | MicroSD Pin | M.2 Pin |
|--------|---------|-------------|---------|
| SDIO_CLK | U1 | J4.5 (CLK) | J2 (SDIO_CLK) |
| SDIO_CMD | U1 | J4.3 (CMD) | J2 (SDIO_CMD) |
| SDIO_D0 | U1 | J4.7 (DAT0) | J2 (SDIO_D0) |
| SDIO_D1 | U1 | J4.8 (DAT1) | J2 (SDIO_D1) |
| SDIO_D2 | U1 | J4.1 (DAT2) | J2 (SDIO_D2) |
| SDIO_D3 | U1 | J4.2 (DAT3/CD) | J2 (SDIO_D3) |
| CARD_DET | U1 | J4.10 (DET_A) | - |
| SHIELD | GND | J4.11 (SHIELD) | - |

### QSPI Bus (Quad SPI Flash Interface)
Connects: **U1 (MCU)** ↔ **J2 (M.2 Socket)**

| Signal | MCU (U1) | M.2 (J2) |
|--------|----------|----------|
| QSPI_CLK | U1 | J2 |
| QSPI_CS | U1 | J2 |
| QSPI_IO0 | U1 | J2 |
| QSPI_IO1 | U1 | J2 |
| QSPI_IO2 | U1 | J2 |
| QSPI_IO3 | U1 | J2 |

### I2C Bus
Connects: **U1 (MCU)** ↔ **J2 (M.2 Socket)**

| Signal | MCU (U1) | M.2 (J2) |
|--------|----------|----------|
| I2C_SCL | U1 | J2 |
| I2C_SDA | U1 | J2 |

### I2S Audio Interface
Connects: **U1 (MCU)** ↔ **J2 (M.2 Socket)**

| Signal | MCU (U1) | M.2 (J2) |
|--------|----------|----------|
| I2S_SCK | U1 | J2 |
| I2S_WS | U1 | J2 |
| I2S_DIN | U1 | J2 |
| I2S_DOUT | U1 | J2 |

### SPI Bus
Connects: **U1 (MCU)** ↔ **J2 (M.2 Socket)**

| Signal | MCU (U1) | M.2 (J2) |
|--------|----------|----------|
| SPI_SCK | U1 | J2 |
| SPI_MOSI | U1 | J2 |
| SPI_MISO | U1 | J2 |
| SPI_CS0 | U1 | J2 |
| SPI_CS1 | U1 | J2 |

### UART Interface
Connects: **U1 (MCU)** ↔ **J2 (M.2 Socket)**

| Signal | MCU (U1) | M.2 (J2) |
|--------|----------|----------|
| UART_TX | U1 | J2 |
| UART_RX | U1 | J2 |

### USB Hub Connections
Connects: **J1 (USB-C)** → **U2 (USB Hub)** → **J2, J3, J5**

| Signal | USB Hub (U2) | Connected To |
|--------|--------------|--------------|
| USB_DP0 | U2 Port 0 | J1 (USB-C D+) |
| USB_DM0 | U2 Port 0 | J1 (USB-C D-) |
| USB_DP1 | U2 Port 1 | J2 (M.2 USB) |
| USB_DM1 | U2 Port 1 | J2 (M.2 USB) |
| USB_DP2 | U2 Port 2 | J3 (RJ45 - Ethernet) |
| USB_DM2 | U2 Port 2 | J3 (RJ45 - Ethernet) |
| USB_DP3 | U2 Port 3 | J5 (USB-A Stack) |
| USB_DM3 | U2 Port 3 | J5 (USB-A Stack) |

### GPIO Connections
Connects: **U1 (MCU)** ↔ **J2 (M.2 Socket)**

| Signal | Direction |
|--------|-----------|
| GPIO0 | Bidirectional |
| GPIO1 | Bidirectional |
| GPIO2 | Bidirectional |
| GPIO3 | Bidirectional |
| GPIO4 | Bidirectional |
| GPIO5 | Bidirectional |

### Control Signals
| Signal | From | To | Purpose |
|--------|------|-----|---------|
| MOD_EN | U1 | J2 | Module Power Enable |
| RST | U1 | J2 | Module Reset |
| IRQ | J2 | U1 | Module Interrupt Request |
| CARD_DET | J2 | U1 | Module Presence Detect |
| LED1 | U1 | J3 | Ethernet LED 1 |
| LED2 | U1 | J3 | Ethernet LED 2 |

### Power Distribution

| Rail | Components |
|------|------------|
| +3V3 | U1, U2, J1, J2, J3, J4, J5, C1-C9 |
| GND | All components |
| VBAT | BT1 → U1 (RTC backup) |

---

## Unconnected Pins by Component

### J2 - M.2 Socket E-Key (OutbackEdge-M2e-Mod-Interface v1.0)

This connector uses the custom **OutbackEdge-M2e-Mod-Interface** standard, NOT standard PC M.2.

**Connection Status: FULLY WIRED** - All mandatory signals are connected to MCU (U1).

**KEY Cutout Pins (No-Connect by Design):**
- Pins 24, 25, 26, 27, 28, 29, 30, 31 - Physically absent in E-key sockets

**Reserved Pins (For Future Expansion):**
- Pin 44 - RESERVED (future: EBI-lite, differential pairs, etc.)
- Pin 46 - RESERVED
- Pin 56 - RESERVED
- Pin 59 - RESERVED
- Pin 61 - RESERVED
- Pins 65, 66, 67, 71 - RESERVED

**Optional Power Rails (Not Connected - Baseboard doesn't provide):**
- Pins 64, 70, 73 - 5V (optional for LTE modules, USB-powered devices)
- Pin 68 - 3V3_AUX (optional standby rail for wake functions)

**Note:** Reserved pins must not be used by modules in v1.0. Optional 5V/3V3_AUX rails require baseboard support.

### J5 - USB 3.0 Type-A Stacked (Dual Port)

**USB 3.0 SuperSpeed Pins (Unconnected - USB 2.0 Only Implemented):**

Port A (Top):
- Pin 5 - SSRX- (SuperSpeed RX-)
- Pin 6 - SSRX+ (SuperSpeed RX+)
- Pin 8 - SSTX- (SuperSpeed TX-)
- Pin 9 - SSTX+ (SuperSpeed TX+)

Port B (Bottom):
- Pin 14 - SSRX- (SuperSpeed RX-)
- Pin 15 - SSRX+ (SuperSpeed RX+)
- Pin 17 - SSTX- (SuperSpeed TX-)
- Pin 18 - SSTX+ (SuperSpeed TX+)

### U2 - USB2514B USB Hub

**Port 4 (Unused):**
- USBDP4 - USB Data Plus Port 4
- USBDM4 - USB Data Minus Port 4

### U1 - Renesas R7FA6M5AH3CFB#AA0 MCU

**Available/Unconnected GPIO Pins:**
Many GPIO pins on the 144-pin MCU are available for expansion. The schematic primarily uses pins for:
- Communication interfaces (SDIO, QSPI, I2C, I2S, SPI, UART)
- USB connections
- Control signals

**Analog Reference Pins (May Need Connection):**
- AVCC0/AVCC1 - Analog VCC (should connect to +3V3)
- AVSS0/AVSS1 - Analog VSS (should connect to GND)
- VREFH/VREFL - ADC voltage reference

### J4 - MicroSD Card Socket

**Detection Pin:**
- Pin 9 (DET_B) - Secondary card detection (may be unconnected if only DET_A used)

**Shield:**
- Pin 11 (SHIELD) - Connect to GND with a short trace and via stitching for EMI control.

### J3 - RJ45 Ethernet Connector

**Shield Pin:**
- SHIELD - Should connect to chassis ground

### J1 - USB Type-C Connector

**CC Pins (Configuration Channel):**
- CC1, CC2 - May need pull-down resistors for UFP mode

**VBUS Detection:**
- VBUS pins may need protection circuitry

### BT1 - Battery Cell

All pins connected (positive to VBAT, negative to GND)

### SW1 - Push Button

All pins connected (one side to MCU GPIO, other to GND)

### C1-C9 - Decoupling Capacitors

All pins connected (typical decoupling between +3V3 and GND)

### R1 - Resistor

All pins connected

---

## Connection Summary Diagram

```
                                    +----------------+
                                    |   J2 (M.2)     |
                                    |   E-Key        |
    +--------+                      |                |
    |  J1    |    +---------+       | SDIO, QSPI,    |
    | USB-C  |--->|   U2    |------>| I2C, I2S, SPI  |
    |        |    | USB Hub |       | UART, GPIO     |
    +--------+    +---------+       | USB            |
                       |            +----------------+
                       |
                       |            +----------------+
                       +----------->|   J3 (RJ45)    |
                       |            |   Ethernet     |
                       |            +----------------+
                       |
                       |            +----------------+
                       +----------->|   J5 (USB-A)   |
                                    |   Stacked      |
                                    +----------------+

    +--------+                      +----------------+
    |  U1    |<-------------------->|   J4 (uSD)     |
    |  MCU   |                      |   MicroSD      |
    +--------+                      +----------------+
        |
        |                           +----------------+
        +-------------------------->|   J3 LEDs      |
        |                           +----------------+
        |
        +---------------------------|   SW1, BT1     |
                                    +----------------+
```

---

## M.2 Socket (J2) Complete Pin Mapping

### Connected Signal Pins

| Pin | Signal | Type | Connected To |
|-----|--------|------|--------------|
| 3 | USB_DP | USB 2.0 | U2 (USB Hub Port 1) |
| 5 | USB_DM | USB 2.0 | U2 (USB Hub Port 1) |
| 6 | LED1 | Output | J3 (Ethernet LED) |
| 8 | I2S_SCK | I2S | U1 (MCU) |
| 9 | SDIO_CLK | SDIO | U1 (MCU), J4 (uSD) |
| 10 | I2S_WS | I2S | U1 (MCU) |
| 11 | SDIO_CMD | SDIO | U1 (MCU), J4 (uSD) |
| 12 | I2S_DIN | I2S | U1 (MCU) |
| 13 | SDIO_D0 | SDIO | U1 (MCU), J4 (uSD) |
| 14 | I2S_DOUT | I2S | U1 (MCU) |
| 15 | SDIO_D1 | SDIO | U1 (MCU), J4 (uSD) |
| 16 | LED2 | Output | J3 (Ethernet LED) |
| 17 | SDIO_D2 | SDIO | U1 (MCU), J4 (uSD) |
| 19 | SDIO_D3 | SDIO | U1 (MCU), J4 (uSD) |
| 20 | MOD_EN | Control | U1 (MCU) |
| 21 | IRQ | Control | U1 (MCU) |
| 22 | UART_RX | UART | U1 (MCU) |
| 23 | RST | Control | U1 (MCU) |
| 32 | UART_TX | UART | U1 (MCU) |
| 34 | GPIO0 | GPIO | U1 (MCU) |
| 35 | SPI_SCK | SPI | U1 (MCU) |
| 36 | GPIO1 | GPIO | U1 (MCU) |
| 37 | SPI_MOSI | SPI | U1 (MCU) |
| 38 | GPIO2 | GPIO | U1 (MCU) |
| 40 | GPIO3 | GPIO | U1 (MCU) |
| 41 | SPI_MISO | SPI | U1 (MCU) |
| 42 | GPIO4 | GPIO | U1 (MCU) |
| 43 | GPIO5 | GPIO | U1 (MCU) |
| 47 | SPI_CS0 | SPI | U1 (MCU) |
| 48 | QSPI_CLK | QSPI | U1 (MCU) |
| 49 | SPI_CS1 | SPI | U1 (MCU) |
| 50 | QSPI_CS | QSPI | U1 (MCU) |
| 52 | QSPI_IO0 | QSPI | U1 (MCU) |
| 53 | QSPI_IO1 | QSPI | U1 (MCU) |
| 54 | QSPI_IO2 | QSPI | U1 (MCU) |
| 55 | QSPI_IO3 | QSPI | U1 (MCU) |
| 58 | I2C_SDA | I2C | U1 (MCU) |
| 60 | I2C_SCL | I2C | U1 (MCU) |
| 62 | CARD_DET | Control | U1 (MCU) |

### Connected Power Pins

| Pin | Signal | Rail |
|-----|--------|------|
| 1, 7, 18, 33, 39, 45, 51, 57, 63, 69, 75 | GND | Ground |
| 2, 4, 72, 74 | 3V3_MAIN | +3V3 (1.0A max) |

---

## Notes

1. **USB Implementation**: Only USB 2.0 is implemented despite J5 having USB 3.0 physical capability
2. **M.2 E-Key Interface**: Uses custom **OutbackEdge-M2e-Mod-Interface v1.0** standard:
   - NOT electrically compatible with PC/laptop PCIe-based M.2 devices
   - Supports SDIO, USB 2.0, SPI, QSPI/OSPI, UART, I2C, and GPIO
   - Designed for MCU-oriented expansion modules (WiFi, LTE, Storage, NPU, GPU, MCU/FPGA)
   - Maximum module power: 1.5W total
   - Hot-plugging NOT supported
3. **Power**: Primary +3V3 rail (1.0A max for M.2 modules) with decoupling capacitors
4. **Battery Backup**: BT1 provides RTC backup power to MCU
5. **Module Detection**: CARD_DET pin pulled low by module when installed
6. **Module Control**: MOD_EN enables module power, RST provides reset, IRQ for interrupts

### Supported M.2 Module Types (OutbackEdge-M2e-Mod-Interface):
- WiFi/Bluetooth modules (SDIO or USB)
- LTE cellular modems (USB)
- Storage expansion (SPI or QSPI/OSPI)
- Neural processing units (SPI or QSPI)
- GPU/Accelerator cards (SPI or QSPI)
- MCU/SoC modules (ESP, RP2040, etc.)

---

*Generated from KiCad schematic: Outback Edge v1.0.kicad_sch*
