# esp32-e22-lora-terminal

Cellular-independent, long-range 433MHz handheld LoRa transceiver built around dual-core **ESP32-S3** microcontrollers and **EBYTE E22-400T33D-V2** (SX1268, 33dBm / 2W) RF modules. Designed for reliable point-to-point text messaging, GPS telemetry, and sensor packet transmission in remote terrain without cellular coverage.

## Hardware Architecture & Upgrade Path
Our initial bench prototype was validated using EBYTE **E32-433T30D-V8** (SX1278) modules. The RF stage is currently being upgraded to the SX1268-based **E22-400T33D-V2** (33dBm / 2W) paired with high-gain **TX433-BLG-40** fiberglass antennas to benchmark higher link budgets, improved receiver sensitivity, and Listen-Before-Talk (LBT) anti-interference performance.

## Bill of Materials (Target Build)
* **Host MCU:** ESP32-S3 (Dual-Core Xtensa LX7 @ 240MHz)
* **RF Transceiver:** EBYTE E22-400T33D-V2 (433MHz, 33dBm / 2W, Semtech SX1268)
* **Antenna:** EBYTE TX433-BLG-40 (433MHz High-Gain Fiberglass Antenna, 50Ω)
* **PC Config Interface:** EBYTE E15-USB-T2 (USB-to-TTL Test Adapter for RF Setting utility)
* **Power Stage:** High-drain Li-ion battery with dedicated 5.0V boost regulation and low-ESR bulk decoupling (470µF electrolytic + 100nF ceramic) to prevent voltage sag during 2W TX bursts.
* **User Interface:** 0.96" I2C OLED display for real-time RSSI/SNR diagnostics and packet status.

## Electrical Interface (ESP32-S3 ↔ E22-400T33D-V2)

| E22 Module Pin | ESP32-S3 Pin | Direction | Notes |
| :--- | :--- | :--- | :--- |
| `VCC` | `5.0V Rail` | Power In | Dedicated 5.0V supply decoupled directly at module pins |
| `GND` | `GND` | Reference | Common star-ground plane |
| `RXD` | `GPIO 17 (TX2)` | MCU → E22 | 3.3V TTL UART serial data input |
| `TXD` | `GPIO 18 (RX2)` | E22 → MCU | 3.3V TTL UART serial data output |
| `AUX` | `GPIO 4` | E22 → MCU | Hardware FIFO buffer status & wake-up interrupt |
| `M0` | `GPIO 5` | MCU → E22 | Operating mode select bit 0 |
| `M1` | `GPIO 6` | MCU → E22 | Operating mode select bit 1 |

## Testing & Documentation Roadmap
1. **Bench Validation & RF Configuration:** Configure air data rate, channel frequency (433MHz), and transmission power parameters via `E15-USB-T2` and EBYTE's official RF Setting utility.
2. **Power Rail Stability Testing:** Measure current draw and voltage ripple across the 5.0V rail during continuous 33dBm (2W) packet bursts.
3. **Field Range Benchmarks:** Conduct line-of-sight (LOS) and obstructed terrain range tests with GPS distance logging, comparing baseline `E32-433T30D-V8` metrics against `E22-400T33D-V2` + `TX433-BLG-40`.
4. **Media & Technical Review:** Publish full assembly walkthroughs, wiring tutorials, and comparative field-test videos.

## Author & Media Channels
* **Developer:** Muhammad Ahsan Nadeem Baig (BS Software Engineering, Virtual University of Pakistan)
* **Location:** Jhelum, Punjab, Pakistan
* **Video Production Portfolio:** [muhammadahsannadeembaig.vercel.app](https://muhammadahsannadeembaig.vercel.app/)
* **YouTube Channel:** [@ryani_edits](https://www.youtube.com/@ryani_edits)
