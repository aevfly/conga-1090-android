# Aplicación Conga 1090 para Android 12+

Este repositorio contiene el archivo APK de la aplicación "Conga S1090/1099", que soluciona el problema de instalación en dispositivos con el sistema operativo Android 12 y versiones superiores.

## Instrucciones de instalación

1. **Desinstala la versión anterior.** Si tienes instalada una versión previa de la aplicación Conga, elimínala desde los ajustes de tu dispositivo.
2. **Descarga el archivo APK.** **[Descarga](https://github.com/aevfly/conga-1090-android/releases/download/v1.0-5/conga.apk)**  la última versión desde este enlace.
3. **Habilita fuentes desconocidas.** Ve a Configuración -> Seguridad y activa "Instalación desde fuentes desconocidas".
4. **Instala el archivo.** Abre el archivo APK descargado en tu administrador de archivos e instálalo.
   
## Problema

La aplicación oficial de Cecotec no se ha actualizado desde 2020 y no es compatible con los nuevos requisitos de seguridad de Android. Al intentar instalarla en Android 12, 13 o 14, es probable que recibas el error "La aplicación no se instaló", ya que el sistema la bloquea debido a la falta de banderas de seguridad obligatorias para las nuevas versiones de Android.

## Solución

Se realizaron los cambios mínimos necesarios en el manifiesto de la aplicación (`AndroidManifest.xml`): se añadió el atributo `android:exported="true"` para todos los componentes que lo requieren, según las reglas de Android 12 (API 31). No se modificaron otros archivos ni funciones de la aplicación.

---

* Todos los derechos sobre la marca "Conga" y el código fuente pertenecen a sus propietarios legales.

---

## ¿Dónde descargar?

Haz clic en la sección **["Releases"](https://github.com/aevfly/conga-1090-android/releases)** en el panel derecho de esta página para encontrar y descargar el archivo APK listo para instalar.

---

###

# Conga 1090 App for Android 12+

This repository contains the APK file for the "Conga S1090/1099" application, which fixes the installation issue on devices running Android 12 and higher.

## Installation Instructions
1. **Uninstall the previous version.** If you have an older version of the Conga app installed, remove it from your device settings.
2. **Download the APK file.** **[Download](https://github.com/aevfly/conga-1090-android/releases/download/v1.0-5/conga.apk)**  the latest version from this link.
3. **Allow unknown sources.** Go to Settings -> Security and enable "Install from unknown sources."
4. **Install the file.** Open the downloaded APK file in your file manager and install it.

## Problem

The official Cecotec app has not been updated since 2020 and is incompatible with Android’s new security requirements. When attempting to install it on Android 12, 13, or 14, you are likely to encounter the error "App not installed" because the system blocks it due to missing mandatory security flags for newer Android versions.

## Solution

The application’s manifest (`AndroidManifest.xml`) was modified with the minimal changes required: the `android:exported="true"` attribute was added to all components that need it, in accordance with Android 12 (API 31) rules. No other files or functionalities of the app were altered.

---

* All rights to the "Conga" trademark and source code belong to their rightful owners.

---

## Where to download?

Click on the **["Releases"](https://github.com/aevfly/conga-1090-android/releases)** section on the right panel of this page to find and download the ready-to-install APK file.

---

Main MCU Firmware & Hardware  
 
Repository contains the full, verified 128 KB raw Flash memory dump (`128.bin`) and its decompiled C source code (`128.c`) for the main microcontroller (MCU) of the Cecotec Conga 1090 and Polaris PVCR 1090 robot vacuums.  
 
This section contains the extracted raw Flash memory dump (`128.bin`) and the decompiled C source code (`128.c`) of the robot's main microcontroller (MCU), responsible for movement and hardware sensors.

### Hardware Specifications

*   **Motherboard Model:** `D330-A-V1.0` (Silkscreen date: `20201010`)
*   **Main Microcontroller (MCU):**
    *   **Core:** 32-bit ARM Cortex-M0 (Little Endian)
    *   **Silicon Family:** STM32F091/STM32F098 equivalent (e.g. `STM32F091RBT6` or `GD32F190RBT6` clone in LQFP64 package)
    *   **Device IDCODE:** `0x10006442` (Register `0x40015800`)
    *   **CPUID Register:** `0x410CC200` (ARM core r0p0)
*   **Memory Capacity:**
    *   **Flash (ROM):** **128 KB** (Reported by hardware register `0x1FFFF7CC` as `0x0080` = 128 KB). The active compiled program code and constant strings occupy **85.3 KB** (up to address `0x0001552F`). The remaining area is empty factory padding (`0xFF`).
    *   **SRAM (RAM):** **32 KB** (Standard for the F09x family).
*   **System Clock:** External **8.000 MHz** quartz crystal (`Y2`).
*   **Debug Protocol:** **SWD (Serial Wire Debug)** via the `J9` header labeled `V+ G C D`.
*   **Unique Device ID (UID):** Mapped at address `0x1FFFF7AC` (12 bytes of unique silicon serial number).

### Memory Mapping & Vector Table
```text
Address       Value         Description
0x08000000    0x20001450    Initial Stack Pointer (SRAM address)
0x08000004    0x080000D1    Reset Handler vector (runs on boot)
0x08000008    0x080000D9    NMI Vector
0x0800000C    0x080000DB    HardFault Vector
```

### Firmware Highlights 

The decompiled code reveals several key structural modules and compiler helper functions:

*   **Compiler Helpmates:** Since Cortex-M0 lacks hardware division, the compiler included software routines:
    *   `__aeabi_uidiv` (unsigned division) at `FUN_080000ec`
    *   `__aeabi_idiv` (signed division) at `FUN_08000118`
    *   `memcpy` and `memset` at `FUN_08000162` and `FUN_08000186`
*   **Main Task Scheduler / Event Loop (`FUN_08000e34`):**
    A classic infinite superloop executing nested periodic tasks based on system flags:
    *   **Periodic Sensor Task:** Increments system ticks, polls the ADC (battery level/voltages), processes gyroscope/accelerometer values, and scans infrared cliff sensors.
    *   **System State Tasks:** Monitors wheel encoders for stalls (`LW_Stall!!!`, `RW_Stall!!!`), controls charging modes (`CC Mode` / `CV Mode` - Constant Current / Constant Voltage), manages cleaning algorithms (`SPRIAL`, `WALLFOLLOW`, `RANDOMBOUNCE`), and controls the buzzer (`LS-1`).
    *   **Wi-Fi Communication:** Parses incoming serial packets from the standalone Tuya WR3 module over UART (listening for the standard Tuya frame header `0x55 0xAA`).
*   **Compilation Timestamp:**
    The binary embeds the exact factory compilation date and time:
    `Apr 30 2020 15:16:04`

---

## File Overview

*   `128.bin` — Complete, non-destructive raw binary dump of the 128 KB Flash memory, extracted successfully via SWD.
*   `128.c` — Decompiled C source code of the entire firmware, generated using Ghidra with the `ARM:LE:32:Cortex` profile.
