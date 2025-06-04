# PBKit501-A — Одноплатный модуль (Allwinner T507-H)

![PBKit501-A](https://pb-embedded.ru/upload/iblock/4b4/4b4be4a324d8b8f9c4c3f47e75d9e04a.png)

**PBKit501-A** — это компактный отладочный комплект на базе мощного четырёхъядерного процессора **Allwinner T507-H**. Модуль состоит из вспомогательной «базовой» платы (PBKit501-A_​BASE), на которой закреплён сам вычислительный блок (PBKit501-A), объединённый с необходимыми интерфейсами и компонентами для быстрой разработки «из коробки».

- Полный модуль (PBKit501-A) можно встраивать в готовое устройство.
- PBKit501-A_​BASE (оценочный комплект) поставляется со всем необходимым (USB-TTL, кабели, адаптер, антенна, батарея и пр.), чтобы сразу начать разработку и тестирование.

---

## Основные характеристики

| Параметр                         | Значение                                                         |
|----------------------------------|------------------------------------------------------------------|
| **Процессор (SoC)**              | Allwinner T507-H, 4×Cortex-A53 до 1.8 ГГц                         |
| **ОЗУ**                           | 2 GB LPDDR4                                                      |
| **Постоянная память (eMMC)**      | 16 GB eMMC (встроенная), поддержка TF-карты                      |
| **ОС (по умолчанию)**             | Linux 4.9 (Ubuntu 18.04), в разработке Android 10                 |
| **Питание**                       | 5 V DC (через разъём питания)                                     |
| **Габариты модуля**               | 60 × 40 × 4 мм                                                     |
| **Температурный диапазон**        | –40 °C…+85 °C (промышл. уровень), 0 °C…+70 °C (коммерческий)       |
| **Интерфейсы отображения**        |  
| • LVDS ×1 (двухканальный, до 1080p) / 24 бит RGB (мультиплексируется) |  
| • HDMI ×1 (HDCP 1.4/2.2, до 4K)                                 |
| **Сетевые интерфейсы**            |  
| • Ethernet 100 Мбит/с (RMII на основной плате)  
• Ethernet 1 Гбит/с (RGMII на базе встроенной карты)               |
| **UART**                         | 6 портов (UART0 – отладочный, остальные – мультиплексируются)      |
| **USB**                          | 4 портa 2.0 (USB OTG ×1, USB Host ×3)                              |
| **SDIO**                         | 2 слота (4-битный режим данных)                                    |
| **I²C**                          | До 5 партнерских шин (часы/данные мультиплексируются)             |
| **I²S / Audio**                  | I²S ×1, линейный выход ×1                                          |
| **ADC**                          |  
| • LRADC (6 бит) ×1 (детекция клавиш)  
• GPADC (8 бит, 1.8 V) ×4                                             |
| **PWM**                          | До 6 каналов (мультиплексируется с другими сигнальными линиями)   |
| **RTC**                          | Встроенный контроллер часов реального времени                     |
| **CVBS**                         | CVBS выход ×1                                                     |
| **Камера**                       | Параллельный CSI ×1, MIPI CSI ×1                                   |
| **CIR (ИК-приёмник)**            | 1 линия                                                            |
| **Драйверы и поддержка (Linux 4.9)** | LPDDR4, eMMC, GPIO, UART, I²C, SDIO, Ethernet (CMAC + EMAC), USB 2.0, KEY, ADC, LINEOUT, Wi-Fi, RTC, HDMI OUT, Touch, двойной LVDS, RGB 24 бит, 4G (модем) |

---

## Комплектация оценочного набора PBKit501-A_BASE

Оценочный комплект включает в себя:

1. **Модуль PBKit501-A_BASE** (с установленным модулем PBKit501-A)  
2. **Антенна Wi-Fi / Bluetooth** (mini-PCB)  
3. **Сетевой кабель Ethernet** (1.5 м, прямой)  
4. **UART-кабель PH2.0** (для соединения с UART-портом модуля)  
5. **USB↔UART-конвертер** (USB-TTL адаптер)  
6. **Блок питания 12 V / 1 A** (сетевой адаптер)  
7. **Набор перемычек / джамперов** (для конфигурации)  
8. **Батарея CR2032 + держатель** (для питания RTC)  
9. **USB-кабель Micro-USB** (для питания платы и загрузки ПО)

---

#!/usr/bin/env bash
#
# test_sysinfo.sh
# Скрипт выводит основные сведения о системе PBKit501-A
#

echo "----------------------------------------"
echo "  PBKit501-A System Information Test"
echo "----------------------------------------"
echo

# CPU: модель и частоты
echo "CPU Information:"
if [ -f /proc/cpuinfo ]; then
    awk -F ': ' '/model name/ {print "  Model:", $2; exit}' /proc/cpuinfo
    awk -F ': ' '/cpu MHz/ {print "  Current CPU MHz:", $2; exit}' /proc/cpuinfo
else
    echo "  /proc/cpuinfo not found!"
fi
echo

# Memory: общая и свободная
echo "Memory Information:"
if command -v free &> /dev/null; then
    free -h | awk 'NR==1{print "  "$0} NR==2{print "  "$0}'
else
    echo "  Команда free не найдена!"
fi
echo

# Disk: корневой раздел
echo "Disk Usage (/):"
if command -v df &> /dev/null; then
    df -h / | awk 'NR==1{print "  "$0} NR==2{print "  "$0}'
else
    echo "  Команда df не найдена!"
fi
echo

# Temperature: CPU temp (если доступно)
echo "Temperature (CPU):"
if [ -f /sys/class/thermal/thermal_zone0/temp ]; then
    rawtemp=$(cat /sys/class/thermal/thermal_zone0/temp)
    cputemp=$(echo "scale=1; $rawtemp/1000" | bc)
    echo "  $cputemp °C"
else
    echo "  Температура не доступна (no thermal_zone0)!"
fi
echo

# Uptime
echo "Uptime:"
if command -v uptime &> /dev/null; then
    uptime | awk '{print "  "$0}'
else
    echo "  Команда uptime не найдена!"
fi
echo

echo "----------------------------------------"
echo "      Test Completed."
echo "----------------------------------------"

---

#!/usr/bin/env python3
"""
blink_gpio.py — простой пример мигания GPIO на PBKit501-A (Allwinner T507-H).
Настройка: на GPIO 13 подключён светодиод катодом на землю.
"""

import time
import os

GPIO_PIN = "13"  # Номер GPIO (в sysfs это «gpio13»)

GPIO_PATH = f"/sys/class/gpio/gpio{GPIO_PIN}"
EXPORT_PATH = "/sys/class/gpio/export"
UNEXPORT_PATH = "/sys/class/gpio/unexport"

def gpio_export(pin):
    if not os.path.isdir(GPIO_PATH):
        with open(EXPORT_PATH, "w") as f:
            f.write(pin)
        time.sleep(0.1)  # дождаться создания файлов

def gpio_unexport(pin):
    if os.path.isdir(GPIO_PATH):
        with open(UNEXPORT_PATH, "w") as f:
            f.write(pin)
        time.sleep(0.1)

def gpio_set_direction(pin, direction):
    dir_path = f"{GPIO_PATH}/direction"
    with open(dir_path, "w") as f:
        f.write(direction)
    time.sleep(0.01)

def gpio_set_value(pin, value):
    val_path = f"{GPIO_PATH}/value"
    with open(val_path, "w") as f:
        f.write(value)

def main():
    print(f"Export GPIO {GPIO_PIN}...")
    gpio_export(GPIO_PIN)

    print("Set direction to 'out'")
    gpio_set_direction(GPIO_PIN, "out")

    print("Blinking LED on GPIO", GPIO_PIN)
    try:
        while True:
            gpio_set_value(GPIO_PIN, "1")
            time.sleep(0.5)
            gpio_set_value(GPIO_PIN, "0")
            time.sleep(0.5)
    except KeyboardInterrupt:
        print("\nStopping blink. Cleaning up...")
    finally:
        gpio_unexport(GPIO_PIN)
        print("GPIO unexported. Exiting.")

if __name__ == "__main__":
    main()

>PBKit501-A на базе Allwinner T507-H — это:

Высокопроизводительный MPU-модуль (4 × A53 @1.8 ГГц),

2 GB LPDDR4 + 16 GB eMMC,

Богатый набор интерфейсов (LVDS/RGB, HDMI, Ethernet, UART, USB, I²C, SPI, I²S, SDIO, Audio, Camera, CVBS, CIR, RTC, ADC, PWM),

Оценочный комплект с USB‐UART адаптером, кабелями и антеннами.

Ниже краткие шаги, чтобы начать:

Подайте 5 В на разъём питания базовой платы.

Подключите USB-UART к консоли или HDMI/дисплей.

Зайдите по UART в терминал (115200 baud) и залогиньтесь (обычно root@pbkit501:~#).

Запустите test_sysinfo.sh (см. выше), чтобы убедиться, что ОС загружена и всё «здорово».

При желании подключите LED к GPIO и запустите Python-скрипт blink_gpio.py для простого теста вывода.

Для полной документации (распиновка, User Manual, схемы) — зайдите в раздел поддержки на официальном сайте PB-Embedded (пароль к Яндекс-диску: PBPARTY).
