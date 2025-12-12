# Utsuwa (うつわ)

**Utsuwa** is a custom-engineered, open-source hardware security key based on the **Pico Fido** firmware. It combines modern FIDO2/WebAuthn security.

Unlike standard keys that use mechanical buttons, **Utsuwa** uses a **Hall Effect Sensor**, allowing for contactless authentication via a magnetic ring or charm.

> Utsuwa (うつわ) comes from the Japanese word for "vessel", symbolizing a container for your digital soul.

---

## Features

* **Core:** Powered by the **Raspberry Pi RP2354A** (Dual Core RISC-V/ARM, Secure Boot, Internal Flash).
* **Auth:** **Contactless Magnetic Trigger** (AH3377 Hall Effect Sensor). Zero moving parts.
* **Visual:** **NeoPixel Glow** (WS2812C-2020) for internal status illumination.
* **Portable:** Ultra-compact USB-A form factor with integrated PCB plug, and space for a keychain attachment.
* **Robust:** ESD protection on USB lines for enhanced durability.

---

## Firmware Configuration

This board runs on the [Pico Fido](https://github.com/polhenarejos/pico-fido) open-source firmware. To support the custom hardware (RP2354A + Hall Effect + WS2812), you must compile the firmware with the following settings in `board_config.h`:

```c
// Flash Size for RP2354A (Internal 2MB)
#define PICO_FLASH_SIZE_BYTES (2 * 1024 * 1024)

// Authentication Button (Hall Effect Sensor)
// Hall Effect pulls Low when magnet is present
#define BUTTON_PIN 18
#define BUTTON_PULL UP 

// Status LED (WS2812C-2020)
#define HAVE_WS2812
#define WS2812_PIN 19
#define WS2812_POWER_PIN -1 // Directly powered by VBUS
```

## Flashing Instructions

    First Time: Short the BOOT pads on the back of the PCB with tweezers while plugging it in.

    Mount: The device will appear as a USB Mass Storage Drive (RPI-RP2).

    Flash: Drag and drop your compiled .uf2 file.

    Reboot: The device will reboot as a FIDO2 Security Key.