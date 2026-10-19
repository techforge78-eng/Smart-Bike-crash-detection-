# Smart Bike Accident Alert System (ESP32)

An ESP32-based device that detects a likely bike accident from accelerometer data and sends an emergency alert with the rider's **live GPS location** to a mobile phone through the Blynk app.

**Status:** Working prototype
**Tools:** ESP32 · C++ (Arduino-style) · I2C · UART · Blynk

---

## Problem

After a bike accident, the rider may be unable to call for help, and responders lose time finding the location. This device automatically detects an impact and sends the location without any input from the rider.

## How it works

1. **Sense:** the accelerometer is read continuously over I2C.
2. **Detect:** if acceleration exceeds `[threshold, e.g. X g]` `[and/or tilt exceeds X°]`, the firmware flags a possible accident.
3. **Locate:** the GPS module (UART) provides the current latitude and longitude.
4. **Alert:** the ESP32 sends the alert and location to the phone through Blynk over Wi-Fi `[or hotspot]`.

```
[Accelerometer] ──I2C──┐
                       ├─► [ESP32] ──Wi-Fi──► [Blynk app / phone]
[GPS module]   ──UART──┘
```

## Hardware

| Part | Details |
|------|---------|
| Microcontroller | ESP32 `[dev board model]` |
| Accelerometer | `[e.g. MPU6050, ADXL345]` |
| GPS | `[e.g. NEO-6M]` |
| Power | `[battery / supply details]` |
| Other | `[buzzer, cancel button, etc.]` |

### Wiring

| Module | Interface | ESP32 pins |
|--------|-----------|------------|
| Accelerometer | I2C | `[SDA / SCL pins]` |
| GPS | UART | `[RX / TX pins]` |

![Prototype](images/prototype.jpg)

## Firmware

- **Language:** C++ (Arduino framework)
- **Libraries:** `[Blynk, TinyGPS++, accelerometer library, etc.]`
- **Setup:** copy `config_example.h` to `config.h` and add your Wi-Fi credentials and Blynk token. **Never commit real credentials.**

### Detection logic

`[Describe in 2-3 lines: how you compute total acceleration, the threshold used, and any debounce or confirmation step.]`

## Results

| Test | Outcome |
|------|---------|
| Simulated impact detection | `[result]` |
| GPS fix time | `[approx. seconds outdoors]` |
| Alert delivery time | `[approx. seconds]` |
| False alarms (bumps, potholes) | `[observations]` |

## Limitations and next steps

- [ ] Add a cancel button or delay to prevent false alarms
- [ ] Use GSM/LTE for alerts where Wi-Fi isn't available
- [ ] Add SMS alerts to emergency contacts
- [ ] Improve detection with tilt and sensor fusion, possibly TinyML
- [ ] Design a custom PCB and enclosure

## Repository structure

```
smart-bike-accident-alert-esp32/
├── firmware/      # ESP32 source code
├── hardware/      # wiring diagram / schematic
├── images/        # photos and screenshots
└── README.md
```

## Author

**Dharineesh T A**, Embedded Hardware & IoT Engineer (fresher)
[LinkedIn](https://linkedin.com/in/dharineesh-thangavel) · [GitHub](https://github.com/techforge78-eng)
