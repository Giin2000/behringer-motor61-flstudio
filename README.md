# 🎹 Behringer MOTOR 61 — FL Studio 20+ Configuration Guide

> **Idioma / Language:** [🇪🇸 Español](#español) | [🇬🇧 English](#english)

---

## Español

### Behringer MOTOR 61 — Guía de Configuración para FL Studio 20 y superior

Guía completa y práctica para configurar el teclado controlador **Behringer MOTOR 61** en **FL Studio 20 y superior**, incluyendo el modo Mackie Control (MC), asignación correcta de puertos MIDI y solución de problemas comunes.

---

### 🚨 Aviso Importante Antes de Empezar

> **⚡ El adaptador de corriente 12V es OBLIGATORIO para que los motores funcionen.**  
> Sin él, el teclado opera como controlador MIDI básico, pero **los faders motorizados quedan completamente desactivados**. Ninguna configuración de software puede compensar la ausencia de alimentación.

---

### 📋 Índice

- [Requisitos del Sistema](#requisitos-del-sistema)
- [Estructura de Puertos MIDI](#estructura-de-puertos-midi)
- [Instalación Rápida](#instalación-rápida)
- [Archivos de Documentación](#archivos-de-documentación)
- [Configuración Avanzada](CONFIGURACION_FL_STUDIO.md)
- [Tabla de Modos MC](MC_MODE_TABLA.md)
- [Solución de Problemas](PROBLEMAS_COMUNES.md)

---

### Requisitos del Sistema

| Componente | Requerimiento |
|---|---|
| FL Studio | 20 o superior |
| Sistema Operativo | Windows 10/11 o macOS 12+ |
| Conexión | USB tipo B |
| Alimentación | Adaptador 12V DC (incluido en caja) |
| Driver | Behringer USB Audio Driver (Windows) / Nativo (macOS) |

---

### Estructura de Puertos MIDI

El MOTOR 61 expone **dos pares de puertos MIDI** al conectarse por USB:

```
┌─────────────────────────────────────────────────────┐
│              BEHRINGER MOTOR 61 — USB                │
├──────────────────┬──────────────────────────────────┤
│  PUERTO 1        │  MOTOR61 / MIDIIN  / MIDIOUT      │
│  (Teclado)       │  → Notas, velocidad, pitch bend   │
│                  │  → Control de parámetros básicos  │
├──────────────────┬──────────────────────────────────┤
│  PUERTO 2        │  MIDIIN2 / MIDIOUT2               │
│  (Mackie Control)│  → Protocolo MC bidireccional     │
│                  │  → Faders, botones, LEDs, motores │
└──────────────────┴──────────────────────────────────┘
```

> **Regla de oro:**  
> - **Puerto 1** → Teclado / Instrumento / Notas  
> - **Puerto 2 (MIDIIN2/MIDIOUT2)** → Control de superficie (Mackie Control)

---

### Instalación Rápida

1. **Conecta** el adaptador 12V DC al MOTOR 61
2. **Conecta** el cable USB al ordenador
3. **Activa MC Mode** en el teclado (ver [MC_MODE_TABLA.md](MC_MODE_TABLA.md))
4. En FL Studio → `Options` → `MIDI Settings`
5. Configura **MIDIIN2** como entrada con `Mackie Control Universal` o script equivalente
6. Configura **MIDIOUT2** como salida con el mismo controlador
7. Habilita el **Puerto 1** (MOTOR61/MIDIIN) para entrada de notas
8. Pulsa **Refresh** y verifica que los faders se mueven al cargar un proyecto

Para instrucciones detalladas: [CONFIGURACION_FL_STUDIO.md](CONFIGURACION_FL_STUDIO.md)

---

### Archivos de Documentación

| Archivo | Descripción |
|---|---|
| [README.md](README.md) | Este archivo — visión general y quickstart |
| [CONFIGURACION_FL_STUDIO.md](CONFIGURACION_FL_STUDIO.md) | Guía paso a paso detallada en FL Studio |
| [MC_MODE_TABLA.md](MC_MODE_TABLA.md) | Tabla completa de funciones en modo MC |
| [PROBLEMAS_COMUNES.md](PROBLEMAS_COMUNES.md) | Diagnóstico y solución de errores frecuentes |
| [PRESETS_GUIA.md](PRESETS_GUIA.md) | Crear, guardar, renombrar y cargar presets (Cap. 10) |
| [ASIGNACION_NOTAS_CC.md](ASIGNACION_NOTAS_CC.md) | Asignar CC y Notas por control en MIDI mode (Cap. 4) |
| [KEYBOARD_MAPPING_FL.md](KEYBOARD_MAPPING_FL.md) | Mapear teclas y pads a sonidos específicos en FL Studio |
| [PERFORMANCE_EN_VIVO.md](PERFORMANCE_EN_VIVO.md) | Guía completa para actuaciones en vivo |

---

### Contribuciones

¿Encontraste algo incorrecto o quieres añadir información?  
Abre un **Issue** o envía un **Pull Request**. ¡Las contribuciones son bienvenidas!

---

## English

### Behringer MOTOR 61 — FL Studio 20+ Configuration Guide

A complete, practical guide for configuring the **Behringer MOTOR 61** keyboard controller in **FL Studio 20 and above**, including Mackie Control (MC) mode, correct MIDI port assignment, and common troubleshooting.

---

### 🚨 Important Notice Before Starting

> **⚡ The 12V DC power adapter is REQUIRED for the motors to work.**  
> Without it, the keyboard functions as a basic MIDI controller, but **the motorized faders are completely disabled**. No software configuration can compensate for the missing power supply.

---

### 📋 Table of Contents

- [System Requirements](#system-requirements)
- [MIDI Port Structure](#midi-port-structure)
- [Quick Setup](#quick-setup)
- [Documentation Files](#documentation-files)

---

### System Requirements

| Component | Requirement |
|---|---|
| FL Studio | 20 or higher |
| Operating System | Windows 10/11 or macOS 12+ |
| Connection | USB Type B |
| Power | 12V DC adapter (included in box) |
| Driver | Behringer USB Audio Driver (Windows) / Native (macOS) |

---

### MIDI Port Structure

The MOTOR 61 exposes **two MIDI port pairs** when connected via USB:

```
┌─────────────────────────────────────────────────────┐
│              BEHRINGER MOTOR 61 — USB                │
├──────────────────┬──────────────────────────────────┤
│  PORT 1          │  MOTOR61 / MIDIIN  / MIDIOUT      │
│  (Keyboard)      │  → Notes, velocity, pitch bend    │
│                  │  → Basic parameter control        │
├──────────────────┬──────────────────────────────────┤
│  PORT 2          │  MIDIIN2 / MIDIOUT2               │
│  (Mackie Control)│  → Bidirectional MC protocol      │
│                  │  → Faders, buttons, LEDs, motors  │
└──────────────────┴──────────────────────────────────┘
```

> **Golden rule:**  
> - **Port 1** → Keyboard / Instrument / Notes  
> - **Port 2 (MIDIIN2/MIDIOUT2)** → Control surface (Mackie Control)

---

### Quick Setup

1. **Connect** the 12V DC adapter to the MOTOR 61
2. **Connect** the USB cable to your computer
3. **Activate MC Mode** on the keyboard (see [MC_MODE_TABLA.md](MC_MODE_TABLA.md))
4. In FL Studio → `Options` → `MIDI Settings`
5. Set **MIDIIN2** as input with `Mackie Control Universal` or equivalent script
6. Set **MIDIOUT2** as output with the same controller
7. Enable **Port 1** (MOTOR61/MIDIIN) for note input
8. Click **Refresh** and verify that faders move when loading a project

For detailed instructions: [CONFIGURACION_FL_STUDIO.md](CONFIGURACION_FL_STUDIO.md)

---

### Documentation Files

| File | Description |
|---|---|
| [README.md](README.md) | This file — overview and quickstart |
| [CONFIGURACION_FL_STUDIO.md](CONFIGURACION_FL_STUDIO.md) | Detailed step-by-step guide in FL Studio |
| [MC_MODE_TABLA.md](MC_MODE_TABLA.md) | Complete function table in MC mode |
| [PROBLEMAS_COMUNES.md](PROBLEMAS_COMUNES.md) | Diagnosis and fix for common issues |
| [PRESETS_GUIA.md](PRESETS_GUIA.md) | Create, save, rename and load presets (Ch. 10) |
| [ASIGNACION_NOTAS_CC.md](ASIGNACION_NOTAS_CC.md) | Assign CC and Notes per control in MIDI mode (Ch. 4) |
| [KEYBOARD_MAPPING_FL.md](KEYBOARD_MAPPING_FL.md) | Map keys and pads to specific sounds in FL Studio |
| [PERFORMANCE_EN_VIVO.md](PERFORMANCE_EN_VIVO.md) | Complete guide for live performances |

---

### Contributing

Found something incorrect or want to add information?  
Open an **Issue** or submit a **Pull Request**. Contributions are welcome!

---

*Documentado con FL Studio 20+ y Behringer MOTOR 61 firmware 1.x — Mayo 2026*  
*Documented with FL Studio 20+ and Behringer MOTOR 61 firmware 1.x — May 2026*
