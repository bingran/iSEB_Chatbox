# iSEB_ChatBox

The user guide will help you get started with iSEB ChatBox and provide more in-depth hardware information.

The **iSEB ChatBox** is an AI development board produced by **INfornique**, based on the  
[ESP32-S3](https://www.espressif.com/en/products/socs/esp32-s3).  
It features:

- 2-Megapixel OV2640 camera  
- SPI TFT LCD display  
- MEMS microphone + ES8388 audio codec  
- Speaker amplifier (MD8002A)  
- 8MB Octal PSRAM  
- 16MB Flash  
- USB Type-C for power, programming, and debugging  
- Multiple I/O including relays, soil sensor, SD card, keys, LEDs

---

# 📑 Table of Contents
1. [Overview](#overview)  
2. [ESP32-S3 Pinout Mapping](#esp32-s3-pinout-mapping)  
   - [LCD SPI Display](#lcd-spi-display)  
   - [Camera OV2640](#camera-ov2640)  
   - [Audio Codec ES8388](#audio-codec-es8388)  
   - [Microphone](#microphone)  
   - [Speaker & Amplifier](#speaker--amplifier)  
   - [SD Card](#sd-card)  
   - [USB-UART (CH340C)](#usb-uart-ch340c)  
   - [IO Expander XL9555](#io-expander-xl9555)  
   - [Keys](#keys)  
   - [LED Indicators](#led-indicators)  
   - [Relays](#relays)   
3. [Related Documents](#Related-Documents)
   - [Datasheet](#Datasheet)
   - [Hardware](#hardware)
   - [Schematic](#schematic)
   - [PCB Layout](#pcb-layout)
4. [Code](#Code)
   - [Example](#Example)
   - [XiaoZhi-ESP32 (iSEB ChatBox Fork)](#xiaozhi-esp32-for-iseb-chatbox)  

---

# Overview

<img width="817" height="522" alt="image" src="https://github.com/user-attachments/assets/733d9a87-b3b2-42aa-a10c-879841ea9e94" />

---

# ESP32-S3 Pinout Mapping

| Pin | GPIO | Remarks     | Pin | GPIO | Remarks     |
|-----|-------|-------------|-----|-------|-------------|
| 1   | GND   | -           | 21  | IO13  | SPI_MISO    |
| 2   | 3V3   | -           | 22  | IO14  | I2S_DOUT    |
| 3   | EN    | RESET       | 23  | IO21  | SLCD_CS     |
| 4   | IO4   | OV_D0       | 24  | IO47  | OV_VSYNC    |
| 5   | IO5   | OV_D1       | 25  | IO48  | OV_HREF     |
| 6   | IO6   | OV_D2       | 26  | IO45  | OV_PCLK     |
| 7   | IO7   | OV_D3       | 27  | IO0   | BOOT        |
| 8   | IO15  | OV_D4       | 28  | IO35  | NC          |
| 9   | IO16  | OV_D5       | 29  | IO36  | NC          |
| 10  | IO17  | OV_D6       | 30  | IO37  | IIC_INT     |
| 11  | IO18  | OV_D7       | 31  | IO38  | OV_SCL      |
| 12  | IO8   | SOIL SENSOR | 32  | IO39  | OV_SDA      |
| 13  | IO19  | USB D−      | 33  | IO40  | IO_SEL      |
| 14  | IO20  | USB D+      | 34  | IO41  | IIC_SDA     |
| 15  | IO3   | I2S_MCLK    | 35  | IO42  | IIC_SCL     |
| 16  | IO46  | I2S_SCK     | 36  | RXD0  | UART RX     |
| 17  | IO9   | I2S_LRCK    | 37  | TXD0  | UART TX     |
| 18  | IO10  | I2S_SDIN    | 38  | IO2   | TF_CS       |
| 19  | IO11  | SPI_MISO    | 39  | IO1   | LED         |
| 20  | IO12  | SPI_SCK     | 40  | GND   | -           |

---

## LCD SPI Display
| Function | ESP32-S3 Pin | Notes |
|---------|--------------|-------|
| SLCD_PWR | XL9555 (IOO_8) | Power enable via expander |
| SLCD_RST | XL9555 (IOO_7) | Reset via expander |
| SLCD_CS | IO21 | SPI chip select |
| SPI_SCK | IO12 | Shared SPI bus |
| SPI_MOSI | IO11 | Shared SPI bus |
| SPI_MISO | IO13 | Optional / Not always used |
| IO_SEL | IO40 | LCD mode select |
| SLCD_RST | IO15 | IRQ |

---

## Camera OV2640
| Function | ESP32-S3 Pin |
|----------|--------------|
| OV_D0 | IO4 | 
| OV_D1 | IO5 |
| OV_D2 | IO6 |
| OV_D3 | IO7 |
| OV_D4 | IO15 |
| OV_D5 | IO16 |
| OV_D6 | IO17 |
| OV_D7 | IO18 |
| OV_VSYNC | IO47 |
| OV_HREF | IO48 |
| OV_PWDN | XL9555 (IOO4)|
| OV_RESET | XL9555 (IOO5) |
| OV_SCL | IO38 (I2C) |
| OV_SDA | IO39 (I2C) |

---

## Audio Codec ES8388
### I2S (Audio)
| Signal | ESP32-S3 Pin |
|--------|--------------|
| I2S_MCLK | IO0 |
| I2S_SCK (BCLK) | IO9 |
| I2S_LRCK | IO8 |
| I2S_SDIN (ADC → ESP) | IO17 |
| I2S_SDOUT (ESP → DAC) | IO18 |

### I2C (Control)
| Signal | ESP32-S3 Pin |
|--------|--------------|
| IIC_SCL | IO1 |
| IIC_SDA | IO2 |

---

## Microphone
- MEMS mic is **analog**, routed to ES8388 ADC pins  
- No direct GPIO connection to ESP32  

---

## Speaker & Amplifier
| Function | Connection |
|----------|------------|
| Speaker Out | MD8002A → 2-pin JST |
| SPK_EN | XL9555 controlled |

---

## SD Card (TF Card)
| Signal | ESP32 Pin |
|--------|-----------|
| SPI_SCK | IO12 | Shared SPI bus |
| SPI_MOSI | IO11 | Shared SPI bus |
| SPI_MISO | IO13 | Shared SPI bus |
| TF_CS | IO2 |

---

## USB-UART (CH340C)
| Signal | ESP32 Pin |
|--------|-----------|
| U0_TXD | IO43 |
| U0_RXD | IO44 |
| USB D+ / D- | Goes to USB Type-C |

---

## LED Indicators
| LED | ESP32 Pin |
|-----|-----------|
| LED1 (Blue) | PWR |
| LED2 (Red) | IO1 |

---

## IO Expander XL9555
Used for:
- LCD Power  
- LCD Reset  
- Camera Reset  
- Camera PWDN  
- Relays  
- Keys  
- LEDs  
- Speaker Enable  

I2C:  
- **SCL = IO1**  
- **SDA = IO2**

| Input | Function | Output | Function |
|-----|-----------|-----|-----------|
| IOI0 | Reserved | IOO0 | Reserved |
| IOI1 | Reserved | IOO1 | Reserved |
| IOI2 | SLCD_RST | IOO2 | SPK_EN |
| IOI3 | SLCD_PWR | IOO3 | Reserved |
| IOI4 | KEY3 | IOO4 | OV_PWDN |
| IOI5 | KEY2 | IOO5 | OV_RESET |
| IOI6 | KEY1 | IOO6 | Relay1 |
| IOI7 | KEY0 | IOO7 | Relay2 |
---

## Keys
| Button | ESP32 Pin |
|--------|-----------|
| KEY0 | XL9555 (IOI7) |
| KEY1 | XL9555 (IOI6) |
| KEY2 | XL9555 (IOI5) |
| KEY3 | XL9555 (IOI4) |

---

## Relays
| Relay | Control Source |
|--------|----------------|
| Relay 1 | XL9555 (IOO7)  |
| Relay 2 | XL9555 (IOO7)  |

---
## Related Documents
### Datasheet

[ESP32-S3 Datasheet (PDF)](https://documentation.espressif.com/esp32-s3_datasheet_en.pdf)

[ESP32-S3-WROOM-1 & ESP32-S3-WROOM-1U Datasheet (PDF)](https://documentation.espressif.com/esp32-s3-wroom-1_wroom-1u_datasheet_en.pdf)

### Hardware
<img width="1057" height="615" alt="image"
src="https://github.com/user-attachments/assets/013eb033-1e56-44cb-aa63-c9c6f0b98903" />

### Schematic
[iSEB_ChatBox_Schematic.pdf](https://github.com/user-attachments/files/23964509/iSEB_ChatBox_Schematic.pdf)

### PCB layout
[iSEB_ChatBox_PCB_layout.pdf](https://github.com/user-attachments/files/23964518/iSEB_ChatBox_PCB_layout.pdf)

---
## Code
### Example

https://github.com/bingran/iSEB_Chatbox/tree/main/Code

### XiaoZhi-ESP32 for iSEB ChatBox

This repository is a **modified fork of the XiaoZhi-ESP32 project** customized for iSEB_ChatBox.  
It enables:

- Wi-Fi connectivity  
- Voice wake word  
- Speech recognition  
- Text-to-speech (TTS)  
- Audio playback  
- OTA firmware updates  

GitHub Repo:  
👉 https://github.com/bingran/xiaozhi-esp32
