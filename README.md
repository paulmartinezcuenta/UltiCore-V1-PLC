# UltiCore V1 - ESP32-Based Industrial PLC 

UltiCore V1 is a high-reliability, industrial-grade Programmable Logic Controller (PLC) custom-designed around the **ESP32-WROOM-32D** architecture. Engineered for harsh electrical environments, this board features high-density optical isolation, dedicated buffered data buses, and a robust power management system.

---

##  Advanced Hardware Architecture & Engineering

### 1. Dual-Bus Data Architecture & Control Logic
* **Buffered Bus Isolation:** Implements octal three-state buffers (**74HC541TS**) to split control signals into dedicated **Power Data Buses** and **Analog Data Buses**. This topology isolates the MCU pins, maximizes fan-out capability, and prevents EMI crosstalk from high-current switching sections.
* **Industrial Output Stage (8-Channel Relay Matrix):** Features 8 independent mechanical relays driven by robust **2N3904** BJT switching circuits. Each channel is equipped with hardwired pull-down networks for deterministic power-up states and **RR1VWM6STFTR** flyback suppression diodes to clamp inductive back-EMF spikes.

### 2. High-Density Input Conditioning & Galvanic Isolation
* **Optically Isolated Digital Inputs:** 8 industrial-level input channels (`IN0`-`IN7`) isolated via high-density **ILD207T** dual optocouplers, establishing complete galvanic separation between the 24V field domain and the 3.3V logic domain.
* **Hardware Debouncing & Waveshaping:** Optocoupler outputs are routed through **74HC14** Hex Schmitt-Trigger inverters to suppress mechanical switch bounce and electrical noise, delivering sharp, clean square waves to the MCU.

### 3. Industrial Power Supply & Protection Framework
* **High-Efficiency Buck Topology:** Integrates an **LM2576HVS-3.3** switching regulator paired with a **100µH** power inductor and a **B330A** Schottky diode to efficiently step down standard industrial 24VDC rails directly to a stable 3.3V rail.
* **Smart Dual-Power Protection (Anti-USB & 24V Cross-Protection):** Utilizes an **LM358DR** operational amplifier comparator circuit coupled with a **PC817** optocoupler and an **FQD11P06** P-Channel MOSFET. This layout actively prevents reverse-current backfeeding and hardware damage when both the high-voltage field power and USB-C programming interface are active simultaneously.
* **Front-End Overcurrent & Polarity Defense:** Equipped with a standard 5x20mm cartridge fuse assembly and a high-current **5S14** blocking diode for reverse-polarity protection.

### 4. Modern Interface & ESD Compliance
* **USB-C Interface:** Modern USB-C implementation driven by a **CH340C** USB-to-UART bridge with an integrated dual-transistor auto-reset/boot-loader circuit.
* **Transient Voltage Suppression:** High-speed **LESD5D5.0CT1G** TVS diode arrays deployed on critical USB data lines (`D+`/`D-`) for localized ESD clamping.

---

## Repository Structure

```text
├── Hardware/        # KiCad schematic captures, multi-layer layout files, and structural BOM
├── Firmware/        # Modular C/C++ source code and RTOS industrial automation tasks
└── Docs/            # Hardware layout sheets, pinout mapping, and component datasheets
