# 🎛️ Asignación de CC y Notas — GLOBAL/MIDI/CHANGE CONTROL

> **← Volver al [README](README.md)**  
> Basado en el **Capítulo 4** del manual oficial del MOTOR 61/49.

---

## Índice

1. [Conceptos Previos](#1-conceptos-previos)
2. [Acceder al Menú CHANGE CONTROL](#2-acceder-al-menú-change-control)
3. [Parámetros Configurables por Control](#3-parámetros-configurables-por-control)
4. [Asignar CC a Faders](#4-asignar-cc-a-faders)
5. [Asignar CC a Encoders](#5-asignar-cc-a-encoders)
6. [Asignar Notas/CC a Pads](#6-asignar-notascc-a-pads)
7. [Asignar CC a los Botones de Transporte](#7-asignar-cc-a-los-botones-de-transporte)
8. [Configurar la Rueda de Modulación](#8-configurar-la-rueda-de-modulación)
9. [Configurar el Pedal de Sustain](#9-configurar-el-pedal-de-sustain)
10. [Configurar el Pedal de Expresión](#10-configurar-el-pedal-de-expresión)
11. [Configurar Fader Touch (SHIFT/FOCUS)](#11-configurar-fader-touch-shiftfocus)
12. [Tabla de Modos de Transporte](#12-tabla-de-modos-de-transporte)
13. [Bancos de Asignaciones](#13-bancos-de-asignaciones)
14. [Guardar Asignaciones en un Preset](#14-guardar-asignaciones-en-un-preset)

---

## 1. Conceptos Previos

### Modo Requerido: MIDI Mode

```
⚠️ CHANGE CONTROL solo está disponible en MIDI mode.
El MC mode tiene asignaciones fijas (protocolo Mackie) que no se pueden editar.

Para activar MIDI mode:
→ Presiona el botón [MIDI] en la sección OPERATION MODE
→ El LED del botón MIDI se ilumina
→ El LED del botón MC se apaga
```

### Tipos de Controles y sus Opciones de Asignación

| Tipo de Control | Puede asignar | Opciones |
|---|---|---|
| Faders (movimiento) | CC | CC 0-127, canal MIDI, rango inicio/fin |
| Faders (toque) | CC o Nota | Igual que botones de pulsación |
| Encoders | CC | CC 0-127, canal MIDI, modo relativo/absoluto |
| Pads | Nota o CC | Nota MIDI o CC, canal, velocidad fija/variable |
| Botones transporte | CC o Nota | Mensaje al presionar y al soltar |
| Mod Wheel | CC | CC 0-127 (predeterminado: CC 1) |
| Sustain Pedal | CC, Nota o función especial | Ver sección 9 |
| Expression Pedal | CC o función especial | Ver sección 10 |

---

## 2. Acceder al Menú CHANGE CONTROL

### Ruta de Acceso

```
[MIDI] (activar MIDI mode)
    ↓
[GLOBAL] (presionar botón GLOBAL)
    ↓
Girar DATA → seleccionar "1. MIDI"
    ↓
Presionar DATA
    ↓
Girar DATA → seleccionar "4. CHANGE CONTROL"
    ↓
Presionar DATA
    ↓
Display: "(WAITING...)" — El teclado espera que muevas el control a configurar
```

> Una vez en el estado **(WAITING...)**, el teclado identifica automáticamente qué control tocas.  
> Simplemente mueve, toca o presiona el control que deseas reasignar.

---

## 3. Parámetros Configurables por Control

Después de tocar el control en modo WAITING, el display te guía por estos parámetros:

### Para Controles Continuos (Faders, Encoders, Mod Wheel, Expression)

```
┌─────────────────────────────────────────────────┐
│  1. MIDI OUT → USB, MIDI, o USB+MIDI            │
│  2. MIDI CH  → 1-16, ALL, GLOBAL CH, o OFF      │
│  3. CC NUM   → 0-127                            │
│     ⚠️ Advertencia si el CC ya está en uso      │
│  4. SET START VALUE → 0-127                     │
│     (valor CC enviado en posición mínima)       │
│  5. SET END VALUE   → 0-127                     │
│     (valor CC enviado en posición máxima)       │
└─────────────────────────────────────────────────┘
```

### Para Controles de Pulsación (Pads, Botones Transporte, Fader Touch)

```
┌─────────────────────────────────────────────────┐
│  Opción A: CTRL CHNG (Control Change)           │
│  ├── MIDI OUT → USB, MIDI, o USB+MIDI           │
│  ├── MIDI CH  → 1-16, ALL, GLOBAL CH, o OFF     │
│  ├── CC NUM   → 0-127                           │
│  ├── ON VALUE → 0-127 (valor al presionar)      │
│  └── OFF VALUE → 0-127 (valor al soltar)        │
│                                                 │
│  Opción B: NOTE MESSAGE (Nota MIDI)             │
│  ├── MIDI OUT → USB, MIDI, o USB+MIDI           │
│  ├── MIDI CH  → 1-16, ALL, GLOBAL CH, o OFF     │
│  ├── NOTE     → C-2 a G8 (nota MIDI)            │
│  └── VELOCITY → 0-127 (fijo) o VARIABLE        │
└─────────────────────────────────────────────────┘
```

> **Navegar entre parámetros:** En cada paso, gira DATA para cambiar el valor, luego presiona DATA para avanzar.  
> Presiona [FWD] para saltar al siguiente control. Presiona [BACK] para salir.  
> Al finalizar, el display muestra "SUCCESS".

---

## 4. Asignar CC a Faders

### Ejemplo: Fader 1 → CC 7 (Volumen de Canal MIDI)

```
PASO 1: Activa MIDI mode → [MIDI]

PASO 2: Accede a CHANGE CONTROL:
  [GLOBAL] → DATA → "1.MIDI" → DATA → "4.CHANGE CONTROL" → DATA
  → Display: "(WAITING...)"

PASO 3: Selecciona el banco del fader
  → Presiona [FADER BANK] "1-8"
  → Ahora mueve el Fader 1 ligeramente
  → Display: "FADER 1"

PASO 4: Presiona DATA → configura:
  MIDI OUT: USB+MIDI → DATA
  MIDI CH: 1 → DATA
  CC NUM: 7 → DATA  (CC7 = Volume)
  START VALUE: 0 → DATA
  END VALUE: 127 → DATA

PASO 5: Display: "SUCCESS"
```

### Tabla de CC Comunes para Faders

| CC | Función estándar MIDI | Uso típico |
|---|---|---|
| 7 | Volume | Volumen de canal del instrumento |
| 11 | Expression | Expresión dinámica |
| 74 | Brightness / Filter Cutoff | Filtro de sintetizador |
| 71 | Resonance | Resonancia de filtro |
| 91 | Reverb Send | Nivel de reverberación |
| 93 | Chorus Send | Nivel de chorus |
| 10 | Pan | Paneo (también disponible en encoders) |
| 1 | Modulation | Modulación (también disponible en Mod Wheel) |

### Rango Invertido (de máximo a mínimo)

Para invertir un fader (arriba = mínimo, abajo = máximo):
```
START VALUE: 127
END VALUE: 0
```

---

## 5. Asignar CC a Encoders

Los encoders funcionan igual que los faders para la asignación de CC, con una diferencia: envían valores relativos por defecto.

### Ejemplo: Encoder 1 → CC 10 (Pan)

```
PASO 1: Activa MIDI mode → [MIDI]

PASO 2: CHANGE CONTROL → (WAITING...)

PASO 3: Selecciona banco de encoders → [ENCODER BANK] "1-8"
  → Gira el Encoder 1
  → Display: "ENCODER 1"

PASO 4: Configura:
  MIDI OUT: USB+MIDI → DATA
  MIDI CH: 1 → DATA
  CC NUM: 10 → DATA  (CC10 = Pan)
  START VALUE: 0 → DATA
  END VALUE: 127 → DATA
```

### Modo de Anillo LED de Encoders (LED Ring Mode)

Independientemente de la asignación CC, cada encoder puede mostrar su valor de forma diferente.  
Accede via: `GLOBAL → ENCODERS → LED RING MODE`

| Modo | Descripción | Ideal para |
|---|---|---|
| SINGLE | Un solo LED indica la posición | Frecuencias, parámetros precisos |
| PAN | LEDs desde el centro hacia los lados | Control de paneo |
| FAN | LEDs desde la izquierda, como un abanico | Volumen, fades |
| SPREAD | LEDs desde el centro hacia ambos lados | Filtros simétricos |
| TRIM | LEDs con indicación de "trim" | Ajustes de ganancia |

---

## 6. Asignar Notas/CC a Pads

Los 8 pads tienen **4 bancos** (PAD BANK 1-8, 9-16, 17-24, 25-32), lo que da hasta **32 pads virtuales** con asignaciones independientes.

### Ejemplo: Pad 1 → Nota C3 (Kick Drum en General MIDI)

```
PASO 1: Activa MIDI mode → [MIDI]

PASO 2: CHANGE CONTROL → (WAITING...)

PASO 3: Selecciona el banco de pads → [PAD BANK] "1-8"
  → Golpea el Pad 1
  → Display: "PAD 1"

PASO 4: Elige el tipo de mensaje:
  → Gira DATA → selecciona "NOTE MESSAGE" → Presiona DATA
  MIDI OUT: USB+MIDI → DATA
  MIDI CH: 10 → DATA  (Canal 10 = percusión en General MIDI)
  NOTE: C3 (nota 36) → DATA  (Kick drum en GM)
  VELOCITY: VARIABLE → DATA  (responde a la fuerza del golpe)

PASO 5: Display: "SUCCESS"
```

### Notas GM de Percusión (Canal 10) — Referencia Rápida

| Nota | # MIDI | Sonido GM |
|---|---|---|
| C3 | 36 | Bass Drum / Kick |
| D3 | 38 | Snare Drum |
| F#3 | 42 | Hi-Hat Cerrado |
| A#3 | 46 | Hi-Hat Abierto |
| C4 | 48 | Tom Bajo |
| E4 | 52 | Tom Medio |
| A4 | 57 | Crash Cymbal |
| D4 | 50 | Tom Alto |

### Asignación CC para Pads (On/Off)

Útil para activar/desactivar parámetros en FL Studio:

```
Tipo: CTRL CHNG
CC NUM: (el que corresponda al parámetro en FL Studio)
ON VALUE: 127  (al presionar)
OFF VALUE: 0   (al soltar)
```

---

## 7. Asignar CC a los Botones de Transporte

Los botones de transporte tienen un modo especial: `TRANSPORT MODE` (GLOBAL → MIDI → 7. TRANSPORT MODE).

### Modos de Transporte Disponibles

| Modo | Descripción |
|---|---|
| **MMC** | MIDI Machine Control — estándar de la industria para DAWs |
| **MIDI** | Mensajes MIDI CC estándar personalizables |
| **MMC+MIDI** | Envía ambos simultáneamente |
| **MIDI Control** | CC con valor fijo al presionar |
| **MIDI Note** | Nota MIDI (ON al presionar, OFF al soltar) |

### Seleccionar el Modo

```
[GLOBAL] → DATA → "1. MIDI" → DATA → "7. TRANSPORT MODE" → DATA
→ Gira DATA para seleccionar el modo
→ Presiona DATA para confirmar
```

### Asignar CC Individualmente a cada Botón de Transporte

Cuando el modo es MIDI, MIDI Control o MIDI Note:

```
CHANGE CONTROL → (WAITING...) → Presiona el botón deseado
(ej. [PLAY], [STOP], [REC], etc.)

Para CTRL CHNG:
  ON VALUE: 127 (al presionar)
  OFF VALUE: 0  (al soltar)

Para NOTE MESSAGE:
  → Elige la nota MIDI que quieres que envíe el botón
```

---

## 8. Configurar la Rueda de Modulación

Por defecto la Mod Wheel envía **CC 1** (Modulation). Para cambiarla:

```
CHANGE CONTROL → (WAITING...)
→ Mueve la rueda de modulación
→ Display: "MOD WHEEL"

Configura:
  MIDI CH: (el canal deseado)
  CC NUM: (el CC deseado, ej. CC 74 para Filter Cutoff)
  START VALUE: 0
  END VALUE: 127
```

---

## 9. Configurar el Pedal de Sustain

El pedal de sustain tiene opciones especiales de función:

```
CHANGE CONTROL → (WAITING...)
→ Presiona el pedal de sustain
→ Display: "SUSTAIN PEDAL"

Opciones de tipo de mensaje:
```

| Opción | Descripción | Uso típico |
|---|---|---|
| `CC MESSAGE` | Envía CC personalizable | Control de parámetro de FL Studio |
| `NOTE MESSAGE` | Envía nota MIDI | Trigger de muestra/instrumento |
| `SUSTAIN PEDAL` | Función sustain estándar (CC 64) | Piano, cuerdas |
| `PLAY/STOP` | Controla reproducción del DAW | Manos libres en estudio |
| `RECORD ON/OFF` | Activa/desactiva grabación | Grabación sin tocar el ratón |
| `ARP ON/OFF` | Activa/desactiva arpeggiador | Performance en vivo |
| `ARP LATCH` | Latch del arpeggiador | Performance con ambas manos libres |

> **Recomendación para directo:** `ARP LATCH` con el pie es ideal para performances en vivo.  
> Mantén notas arpegiando sin necesidad de sujetar las teclas.

---

## 10. Configurar el Pedal de Expresión

El pedal de expresión ofrece opciones de función predefinidas:

```
CHANGE CONTROL → (WAITING...)
→ Mueve el pedal de expresión
→ Display: "EXPR PEDAL"

Opciones:
```

| Opción | Descripción |
|---|---|
| `CC MESSAGE` | Envía CC personalizable (CC 0-127) |
| `EXPRESSION PEDAL` | Expresión estándar (CC 11) |
| `PITCH BEND` | Controla el pitch bend con el pie |
| `MOD WHEEL` | Controla la modulación con el pie (CC 1) |
| `VOLUME` | Volumen de canal (CC 7) |

> **Tip de producción:** Asigna el pedal a Filter Cutoff (CC 74) para  
> hacer sweeps de filtro en tiempo real durante la grabación.

---

## 11. Configurar Fader Touch (SHIFT/FOCUS)

Cada fader tiene **dos comandos de toque** independientes:
- **Toque normal** → el comando principal del fader touch
- **Toque con SHIFT / FOCUS** → un comando alternativo

### Asignar el Comando de Toque Alternativo

```
CHANGE CONTROL → (WAITING...)
→ Mantén presionado [FADER SHIFT] (o activa [FADER FOCUS])
→ Toca (sin mover) el fader deseado
→ El display identifica: "FADER TOUCH X (SHIFT)"

Configura el CC o Nota para la función alternativa
```

### Diferencia entre SHIFT y FOCUS

| Botón | Comportamiento |
|---|---|
| **FADER SHIFT** | Hay que mantenerlo presionado para activar la función alternativa |
| **FADER FOCUS** | Toggle — activa la función alternativa de forma permanente hasta pulsarlo de nuevo |

### Desactivar el Fader Touch

Si no quieres que el toque del fader envíe mensajes MIDI:

```
CHANGE CONTROL → tocar fader deseado → Display: "FADER TOUCH X"
→ MIDI CH: OFF → presionar DATA varias veces hasta "SUCCESS"
```

> **Nota:** `GLOBAL → FADERS → TOUCH ON/OFF` desactiva el touch para todos los faders  
> en ambos modos (MIDI y MC). Para solo desactivarlo en MIDI mode, usa CHANGE CONTROL individualmente.

---

## 12. Tabla de Modos de Transporte

Resumen visual de los 5 modos de transporte:

```
TRANSPORT MODE:
┌──────────────┬──────────────────────────────────────────────────────┐
│ MMC          │ MIDI Machine Control. Compatible con mayoría de DAWs │
│              │ incluyendo FL Studio. Protocolo SysEx estándar.      │
├──────────────┼──────────────────────────────────────────────────────┤
│ MIDI         │ CC estándar asignado libremente por el usuario.      │
│              │ Máxima flexibilidad. Requiere mapeo en FL Studio.    │
├──────────────┼──────────────────────────────────────────────────────┤
│ MMC+MIDI     │ Envía ambos. Útil para compatibilidad con hardware    │
│              │ y software simultáneamente.                          │
├──────────────┼──────────────────────────────────────────────────────┤
│ MIDI Control │ Botón envía valor CC fijo. No hay toggle.            │
│              │ Útil para triggers puntuales en FL Studio.           │
├──────────────┼──────────────────────────────────────────────────────┤
│ MIDI Note    │ Note On al presionar, Note Off al soltar.            │
│              │ Ideal para FL Studio Piano Roll / Pattern triggers.  │
└──────────────┴──────────────────────────────────────────────────────┘
```

---

## 13. Bancos de Asignaciones

El MOTOR 61 tiene **4 bancos** para faders, encoders y pads en MIDI mode, duplicando las asignaciones disponibles:

```
FADERS:  4 bancos × 8 faders = 32 asignaciones únicas de movimiento
         4 bancos × 8 faders = 32 asignaciones únicas de toque
         (+ SHIFT/FOCUS duplica = hasta 128 asignaciones de toque)

ENCODERS: 4 bancos × 8 encoders = 32 asignaciones CC únicas

PADS:    4 bancos × 8 pads = 32 pads virtuales con nota/CC único
```

> **Al asignar CC en un banco específico:**  
> Siempre selecciona primero el banco con [FADER BANK], [ENCODER BANK] o [PAD BANK]  
> ANTES de entrar en CHANGE CONTROL y tocar el control.  
> De lo contrario asignarás el banco 1-8 por defecto.

---

## 14. Guardar Asignaciones en un Preset

**Las asignaciones CHANGE CONTROL se pierden si no guardas el preset.**

```
Después de hacer todas las asignaciones:

1. Verifica que los controles funcionan como esperas en FL Studio

2. Guarda como preset:
   [EDIT] → DATA → "1. PRESETS" → DATA → "1. SAVE/COPY PRESET"
   → Elige número de destino → YES → SUCCESS

3. Renombra el preset para identificarlo:
   [EDIT] → "3. RENAME PRESET" → nombre descriptivo → [FWD]

4. (Opcional) Exporta por SysEx como backup:
   [EDIT] → "5. SYSEX TX" → ALL o SINGLE → YES
```

---

> **Ver también:**
> - [PRESETS_GUIA.md](PRESETS_GUIA.md) — Gestión completa de presets
> - [KEYBOARD_MAPPING_FL.md](KEYBOARD_MAPPING_FL.md) — Mapeo en FL Studio 20+
> - [PERFORMANCE_EN_VIVO.md](PERFORMANCE_EN_VIVO.md) — Asignaciones para directo
