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

Haz clic en la sección **"Releases"** en el panel derecho de esta página para encontrar y descargar el archivo APK listo para instalar.

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

Click on the **"Releases"** section on the right panel of this page to find and download the ready-to-install APK file.

---
