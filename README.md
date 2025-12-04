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
2. [Block diagram](#block-diagram)
3. [XiaoZhi-ESP32 (iSEB ChatBox Fork)](#xiaozhi-esp32-for-iseb-chatbox)  
4. [ESP32-S3 Pinout Mapping](#esp32-s3-pinout-mapping)  
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
5. [Power System](#power-system)

---

# Overview

<img width="817" height="522" alt="image" src="https://github.com/user-attachments/assets/733d9a87-b3b2-42aa-a10c-879841ea9e94" />

---

# Block diagram
<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/ae496111-835d-4f41-b5e6-b733e7055338" />

# XiaoZhi-ESP32 for iSEB ChatBox

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

# ESP32-S3 Pinout Mapping

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
| OV_PCLK | IO45 |
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
| CMD | IO4 |
| CLK | IO5 |
| DATA0 | IO6 |
| DATA1 | IO7 |
| DATA2 | IO15 |
| DATA3 | IO16 |
| TF_CS | IO45 |

---

## USB-UART (CH340C)
| Signal | ESP32 Pin |
|--------|-----------|
| U0_TXD | IO43 |
| U0_RXD | IO44 |
| USB D+ / D- | Goes to USB Type-C |

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

---

## Keys
| Button | ESP32 Pin |
|--------|-----------|
| KEY0 | IO46 |
| KEY1 | IO47 |
| KEY2 | IO48 |
| KEY3 | XL9555 |

---

## LED Indicators
| LED | ESP32 Pin |
|-----|-----------|
| LED1 (Blue) | IO3 |
| LED2 (Red) | IO14 |

---

## Relays
| Relay | Control Source |
|--------|----------------|
| Relay 1 | XL9555 |
| Relay 2 | XL9555 |


Just tell me!
