# PBKit501-A: Одноплатный модуль на базе Allwinner T507-H

![PBKit501-A](https://pb-embedded.ru/upload/iblock/4b4/4b4be4a324d8b8f9c4c3f47e75d9e04a.png)

**PBKit501-A** — это компактный отладочный модуль (SOM) от PB-Embedded, построенный вокруг мощного четырехъядерного процессора **Allwinner T507-H**. В сочетании с базовой платой **PBKit501-A_BASE** он предоставляет полный набор интерфейсов, необходимых для быстрого старта в проектах IoT, мультимедиа, embedded Linux и машинного обучения.

---

## Содержание статьи

1. [Краткое описание](#краткое-описание)  
2. [Технические характеристики](#технические-характеристики)  
3. [Аппаратная платформа](#аппаратная-платформа)  
4. [Комплектация набора PBKit501-A_BASE](#комплектация-набора-pbkit501-a_base)  
5. [Схема питания](#схема-питания-и-разводка)  
6. [Пример Python-скрипта на GPIO](#пример-python-скрипта-на-gpio)  
7. [Заключение](#заключение)  

---

## Краткое описание

PBKit501-A — это System-on-Module (SoM) для встраиваемых приложений, основанный на Allwinner T507-H (4×Cortex-A53 до 1.8 ГГц). Модуль имеет встроенные **2 GB LPDDR4**, **16 GB eMMC** и полный набор интерфейсов:

- Ethernet (100 Мбит+1 Гбит),  
- HDMI 4K,  
- LVDS 1080p,  
- USB 2.0 ×4 (OTG ×1, Host ×3),  
- I²C ×5, SPI ×2, UART ×6,  
- I²S, Audio LINEOUT, ADC ×4, PWM ×6,  
- CSI (MIPI + параллельный), CVBS, CIR, RTC, GPIOs.  

Благодаря базовой плате **PBKit501-A_BASE** вы получаете готовую к отладке платформу с USB-UART, Ethernet, слотом microSD, разъёмом питания и разъёмами для дисплея и камер.

---

## Технические характеристики

| Параметр                        | PBKit501-A (SoM)                                   |
|---------------------------------|----------------------------------------------------|
| **SoC**                         | Allwinner T507-H (4×Cortex-A53 @1.8 ГГц, NPU)       |
| **ОЗУ (LPDDR4)**                | 2 GB                                               |
| **ПЗУ (eMMC)**                  | 16 GB (передустановленный образ Linux)             |
| **MicroSD**                     | 1 слот SD 4-битный                                  |
| **Wi-Fi / Bluetooth**           | 802.11 ac + Bluetooth 5.0 LE                       |
| **Ethernet**                    | 100 Мбит (RMII) + 1 Гбит (RGMII)                   |
| **USB**                         | OTG 2.0 ×1, Host 2.0 ×3                            |
| **HDMI**                        | HDMI 1.4/2.0 до 4K 30 fps                           |
| **LVDS / RGB24 бит**            | 1×LVDS 2-канальный (1080p) или RGB 24 бит          |
| **Audio**                       | I²S ×1, LINEOUT ×1                                 |
| **CSI (камера)**                | 1×MIPI CSI, 1×Parallel CSI                         |
| **CVBS (композит)**             | 1 линия                                           |
| **I²C / SPI / UART**            | I²C ×5, SPI ×2, UART ×6                            |
| **ADC / PWM**                   | ADC 6-бит ×1 (LRADC), ADC 8-бит ×4 (GPADC), PWM ×6  |
| **RTC**                         | Встроенный с батарейным питанием (CR2032)           |
| **Температурный диапазон**      | –40…+85 °C (промышленный) / 0…+70 °C (коммерческий)  |
| **Питание**                     | 5 V DC (через разъем Jack), LDO 3.3 V для SoC       |
| **Габариты SoM**                | 60 × 40 × 4 мм                                      |
| **Габариты базовой платы**      | 100 × 80 × 12 мм                                    |

---

## Аппаратная платформа

### 1. SoC Allwinner T507-H

- 4 × ARM Cortex-A53 @ 1.8 ГГц (64-бит), поддерживает NEON/FPV4.  
- Встроенный NPU (Neural Processing Unit) для TinyML, до 0.5 TOPS.  
- Контроллер памяти LPDDR4, шина 32 бит, до 4 Гбит.  
- Интерфейсы eMMC 5.1, SDIO, SPI, I²C, I²S, PWM, GPIO, ADC, DRAM.

### 2. Память

- **2 GB LPDDR4** — оперативная память высокого быстродействия.  
- **16 GB eMMC** — встроенный флеш-накопитель, на котором предустановлен Linux (Ubuntu 18.04).  
- **MicroSD слот** — поддерживает UHS-I, до 256 GB. Используется для загрузки/расширения.

### 3. Интерфейсы

- **Ethernet 100 Мбит/1 Гбит** — два PHY, один на RMII (100 Мбит) и один на RGMII (1 Гбит).  
- **HDMI 1.4/2.0** — видео-выход до 4K 30 fps, поддержка HDCP 1.4/2.2.  
- **LVDS 24 бит** — два канала, до 1080p, либо RGB 24 бит.  
- **USB 2.0** — один порт OTG, три порта Host (через USB hub).  
- **I²S ×1**, **LINEOUT ×1** — цифровой аудио-интерфейс и аналоговый выход.  
- **CSI** — один MIPI CSI, один параллельный CSI для камер *.  
- **CVBS **— композитный видео-выход (1 линия).  
- **UART ×6** — один отладочный (UART0 → USB-TTL), остальные мультиплексируются.  
- **I²C ×5** — пять шин I²C, могут быть использованы для датчиков, RTC, расширителей портов.  
- **SPI ×2**, **GPIO ×34** — универсальные цифровые линии.  
- **ADC** — LRADC (6 бит) для клавиш/датчиков, GPADC (8 бит, 1.8 V) ×4 для внешних аналогов.  
- **PWM ×6** — ШИМ-выходы для подсветки, моторов, сервоприводов.  
- **RTC** — встроенный контроллер часов, питание от батареи CR2032.  
- **CIR** — ИК-приёмник для дистанционного управления.  

---

## Комплектация набора PBKit501-A_BASE

1. **SoM PBKit501-A** (Allwinner T507-H + RAM + eMMC)  
2. **Базовая плата PBKit501-A_BASE**:
   - USB-UART (CP2102 или CH9102F) для консоли.  
   - 5 V DC Jack (разъем) и LDO → 3.3 V.  
   - Ethernet RJ45 (100 Мбит/1 Гбит).  
   - HDMI Type A Выход.  
   - LVDS/RGB коннектор (40-pin LVDS/RGB).  
   - CSI коннектор (15-pin MIPI Camera).  
   - MicroSD socket (4-bit, UHS-I).  
   - Кнопки BOOT (GPIO 0), RESET (EN).  
   - RTC Battery Holder (CR2032).  
   - Разъемы «по категориям»: GPIO (2×20-pin 2.54 mm), I²C, SPI, PCM, ADC.  
   - Антенна Wi-Fi/BLE (u.FL + mini PCB).  
   - Набор джамперов для выбора режима загрузки, отображения LVDS/RGB, питания и др.

3. **Кабели и аксессуары**:
   - **USB A → Micro-USB** (питание и загрузка).  
   - **USB-TTL Serial Cable** (PH2.0 к CP2102/CH9102F).  
   - **Ethernet Cat5e Cable** (1.5 m).  
   - **Антенна Wi-Fi/BLE** (2 dBi, mini-PCB).  
   - **Блок питания 12 V 1 A** (разъем 5.5/2.1 mm).  
   - **Пара джамперов** (штырьки для разного режима BOOT, LVDS/RGB).  
   - **Инструкция + даташиты** (набор PDF).

---

## Схема питания 
    RTC CR2032 Battery  → VBAT (1.8 V RTC regulator)  
    USB-A → Micro-USB (5 V) → USB-UART → CP2102/CH9102F → UART0 на SoM  
    Ethernet RJ45 ↔ PHY (PHY1 100 Mbit, PHY2 1 Gbit) → GMAC на SoM  
    HDMI Type A → HDMI TX на SoM  
    LVDS 40-pin → LVDS/RGB MUX на SoM  
    Cameras 15-pin CSI → MIPI/CSI на SoM  
---
## Работа с GPIO
```
#!/usr/bin/env python3

blink_gpio.py — мигание LED на GPIO12 (Allwinner T507-H, PBKit501-A)
Требует root-доступ. Пароль смотрите в нашей документации, он однотипный для всех проектов.При желании задайте совй новый пароль.

import time
import os

# Задайте номер GPIO (на Allwinner это gpioX, где X = номер).
GPIO_PIN = "12"
GPIO_PATH = f"/sys/class/gpio/gpio{GPIO_PIN}"
EXPORT_PATH = "/sys/class/gpio/export"
UNEXPORT_PATH = "/sys/class/gpio/unexport"

def gpio_export(pin):
    if not os.path.exists(GPIO_PATH):
        with open(EXPORT_PATH, "w") as f:
            f.write(pin)
        time.sleep(0.1)

def gpio_unexport(pin):
    if os.path.exists(GPIO_PATH):
        with open(UNEXPORT_PATH, "w") as f:
            f.write(pin)
        time.sleep(0.1)

def gpio_set_direction(pin, direction):
    dir_file = f"{GPIO_PATH}/direction"
    with open(dir_file, "w") as f:
        f.write(direction)
    time.sleep(0.01)

def gpio_set_value(pin, value):
    val_file = f"{GPIO_PATH}/value"
    with open(val_file, "w") as f:
        f.write(value)

def main():
    print(f"Экспортируем GPIO {GPIO_PIN}...")
    gpio_export(GPIO_PIN)

    print("Устанавливаем направление 'out'...")
    gpio_set_direction(GPIO_PIN, "out")

    print("Мигаем LED (GPIO {}) example.format(GPIO_PIN))
    try:
        while True:
            gpio_set_value(GPIO_PIN, "1")
            time.sleep(0.5)
            gpio_set_value(GPIO_PIN, "0")
            time.sleep(0.5)
    except KeyboardInterrupt:
        print( "Освобождаем GPIO")
    finally:
        gpio_unexport(GPIO_PIN)
        print("GPIO снят. Завершаем.")
``` 



---
# Заключение 
#№PBKit501-A на базе Allwinner T507-H — это:
Высокопроизводительный MPU-модуль (4 × A53 @1.8 ГГц),
2 GB LPDDR4 + 16 GB eMMC,
Богатый набор интерфейсов (LVDS/RGB, HDMI, Ethernet, UART, USB, I²C, SPI, I²S, SDIO, Audio, Camera, CVBS, CIR, RTC, ADC, PWM),
При желании подключите LED к GPIO и запустите Python-скрипт blink_gpio.py для простого теста вывода.
Для полной документации (распиновка, User Manual, схемы) — зайдите в раздел поддержки на официальном сайте PB-Embedded (пароль к Яндекс-диску: PBPARTY).

> **Примечание:** Все рекомендации относятся к разводке PCB и выбору компонентов для обеспечения надёжности, EMC-совместимости и простоты отладки. Следуйте этим правилам, чтобы минимизировать проблемы при производстве и эксплуатации платы A50I.
> > Все технические файлы Вы можете найти на нашем сайте: https://pb-embedded.ru/?ysclid=mb0xwcpmmj97014171
> Также мы есть в Telegram: [Скорее напишите нам](https://t.me/PBPOLAR)

