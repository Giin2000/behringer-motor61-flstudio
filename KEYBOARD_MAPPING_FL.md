# 🎹 Mapeo de Teclado en FL Studio 20 y Superior

> **← Volver al [README](README.md)**

---

## Índice

1. [Cómo Llegan las Notas a FL Studio](#1-cómo-llegan-las-notas-a-fl-studio)
2. [Asignar el MOTOR 61 como Teclado de Entrada](#2-asignar-el-motor-61-como-teclado-de-entrada)
3. [Mapear Teclas a Instrumentos del Channel Rack](#3-mapear-teclas-a-instrumentos-del-channel-rack)
4. [Keyboard Mapping por Nota — Piano Roll](#4-keyboard-mapping-por-nota--piano-roll)
5. [Distribuir Zonas por Split de Teclado](#5-distribuir-zonas-por-split-de-teclado)
6. [Mapeo de Pads a Sonidos de Batería](#6-mapeo-de-pads-a-sonidos-de-batería)
7. [Usar Program Change para Cambiar Instrumentos](#7-usar-program-change-para-cambiar-instrumentos)
8. [MIDI Learn en Plugins de FL Studio](#8-midi-learn-en-plugins-de-fl-studio)
9. [Guardar el Mapeo como Proyecto Template](#9-guardar-el-mapeo-como-proyecto-template)
10. [Referencia de Notas MIDI](#10-referencia-de-notas-midi)

---

## 1. Cómo Llegan las Notas a FL Studio

El MOTOR 61 usa **Puerto 1** para enviar notas al teclado, y **Puerto 2** para el protocolo Mackie Control. Esto es clave para el mapeo:

```
MOTOR 61 Hardware
│
├── Puerto 1 (MOTOR61 / MIDIIN)         ← Para notas del teclado y pads
│   → Canal MIDI 1-16 (configurable)
│   → Notas: Do-2 a Sol8
│   → Velocity: 0-127 (sensible a la pulsación)
│   → Aftertouch: polyphonic pressure
│   → Pitch Bend, Mod Wheel, CC
│   → Destino en FL Studio: Instrumentos en Channel Rack
│
└── Puerto 2 (MIDIIN2 / MIDIOUT2)       ← Solo protocolo MC (no usar para notas)
    → Destino en FL Studio: Mackie Control Surface
    → NO conectar a instrumentos virtuales
```

### Configuración Mínima en FL Studio

```
Options → MIDI Settings → INPUT:
├── MOTOR61 (puerto 1): ✅ Habilitado, sin controller type específico
└── MIDIIN2 (puerto 2): ✅ Habilitado, Controller: Mackie Control Universal
```

---

## 2. Asignar el MOTOR 61 como Teclado de Entrada

### Paso 1: Verificar la Recepción de Notas

```
1. Abre FL Studio
2. Crea un instrumento en el Channel Rack:
   → Channel Rack → clic derecho → "Add one" → elige un instrumento (ej. FLEX o BassDrum)

3. El canal debe estar seleccionado (fondo verde en Channel Rack)

4. Toca una tecla en el MOTOR 61
   → Debes ver actividad en el medidor de nivel del canal
   → Debes escuchar el instrumento

5. Si no suena: Options → MIDI Settings → verifica que MOTOR61 esté habilitado
```

### Paso 2: Fijar el Canal MIDI de Entrada

Por defecto FL Studio acepta notas en **todos los canales MIDI** del puerto habilitado. Para ser más selectivo:

```
En el Channel Rack, cada instrumento tiene un selector de canal MIDI:
→ Clic derecho en el nombre del canal → "Channel settings"
→ En la ventana del instrumento → pestaña MIDI
→ "Input port" y "MIDI Channel" → ajusta según necesites
```

> **Recomendación:** Deja el canal en "0" (todos) para el teclado principal,  
> y usa canales específicos (1, 2, 3...) solo si tienes múltiples dispositivos.

---

## 3. Mapear Teclas a Instrumentos del Channel Rack

### Método A: Un instrumento, todo el teclado

La configuración más simple: todas las teclas del MOTOR 61 tocan el instrumento seleccionado en verde en el Channel Rack.

```
Channel Rack → clic en el nombre del instrumento para seleccionarlo (se pone verde)
→ Todas las teclas del MOTOR 61 tocan ese instrumento
→ Para cambiar a otro instrumento: clic en el otro canal del Channel Rack
```

### Método B: Arpegio + Notas simultáneas con Split del MOTOR 61

El MOTOR 61 tiene split de teclado incorporado (ver [ASIGNACION_NOTAS_CC.md](ASIGNACION_NOTAS_CC.md)):

```
MOTOR 61: EDIT → KEYBOARD SPLIT → SET UP SPLIT
→ Elige la tecla divisoria (ej. C4)
→ Zona izquierda: Canal MIDI 2 (ej. bajo)
→ Zona derecha: Canal MIDI 1 (ej. melodía)

En FL Studio:
→ Instrumento de bajo: Channel settings → MIDI Input Channel = 2
→ Instrumento de melodía: Channel settings → MIDI Input Channel = 1
```

### Método C: Múltiples Instrumentos por Nota Específica (Piano Roll)

Para asignar notas exactas a sonidos específicos dentro de un plugin de batería o sampler:

```
1. Abre el instrumento en FL Studio (ej. FPC, DrumSynth, o un sampler)

2. En el plugin FPC (FL's pad controller):
   → Arrastra samples a cada pad del FPC
   → Cada pad tiene una nota asignada (C4, D4, E4, etc.)
   → Las teclas del MOTOR 61 que correspondan a esas notas activarán ese pad

3. Para ver qué nota activa qué pad:
   → Clic derecho en un pad de FPC → "Set target note"
   → Asígnale la nota que quieres usar del MOTOR 61
```

---

## 4. Keyboard Mapping por Nota — Piano Roll

FL Studio permite editar con precisión qué nota del teclado activa qué sonido dentro de un plugin compatible con mapeo de notas (como samplers o baterías).

### Con Fruity Keyboard Controller

Esta herramienta de FL Studio permite mapear rangos de notas a parámetros o instrumentos:

```
Channel Rack → clic derecho → Add one → Fruity Keyboard Controller

En el Fruity Keyboard Controller:
→ Define el rango de notas (Start Note / End Note)
→ Conecta la salida a un parámetro de otro plugin
→ Ej: Notas C2-C3 controlan el parámetro "Cutoff" del filtro de un sintetizador
```

### Mapeo Directo en Samplers (FruityLoops / DirectWave)

```
DirectWave (sampler avanzado de FL Studio):
1. Abre DirectWave en el Channel Rack
2. Carga samples en el mapa de zonas (Zone Map)
3. Arrastra/ajusta las zonas de notas para cada sample:
   → Zona 1: C2-B2 → sample de bajo
   → Zona 2: C3-B3 → sample de medio
   → Zona 3: C4-B4 → sample de agudo
4. Las teclas del MOTOR 61 activan el sample de su zona correspondiente
```

---

## 5. Distribuir Zonas por Split de Teclado

### Split en el MOTOR 61 (hardware)

```
[EDIT] → DATA → "KEYBOARD SPLIT" → DATA
→ "1. SPLIT ON/OFF" → ON
→ "2. SET UP SPLIT" → presiona la tecla de división (ej. C4)
→ "LOWER MIDI CHANNEL" → selecciona el canal (ej. Canal 2)
→ "LOWER OCTAVE" → ajusta si necesitas desplazamiento de octava

Resultado:
← C2 a B3 : Canal MIDI 2 (zona izquierda)
   C4 a C7 → : Canal MIDI 1 = GLOBAL CHANNEL (zona derecha)
```

### Configuración Complementaria en FL Studio

```
Para el instrumento de la zona izquierda (ej. bajo):
→ Channel Rack → nombre del canal → doble clic → Channel settings
→ Pestaña MIDI → Input Channel: 2

Para el instrumento de la zona derecha (ej. piano):
→ Channel Rack → nombre del canal → Channel settings
→ Pestaña MIDI → Input Channel: 1 (o GLOBAL CH del MOTOR 61)
```

### Split de 3 Zonas (avanzado)

El MOTOR 61 tiene split de 2 zonas por hardware. Para 3 o más zonas, combina el split del MOTOR 61 con el mapeo de canales en FL Studio:

```
Zona A (Bajo): C1-B2 → Canal MIDI 2 → instrumento de bajo en FL
Zona B (Piano): C3-B4 → Canal MIDI 1 → piano en FL
Zona C (Solo):  C5-C7 → Canal MIDI 1 (mismo que piano, pero rango diferente
                 → FL Studio filtra por rango de notas en el plugin)
```

---

## 6. Mapeo de Pads a Sonidos de Batería

Los **8 pads** del MOTOR 61 (con 4 bancos = 32 pads virtuales) son ideales para controlar baterías en FL Studio.

### Configuración Recomendada con FPC (FL Studio Pad Controller)

```
PASO 1: En MOTOR 61 (MIDI Mode):
  [GLOBAL] → MIDI → CHANGE CONTROL → (WAITING...)
  → Selecciona PAD BANK 1-8
  → Golpea Pad 1 → Asigna:
    TYPE: NOTE MESSAGE
    MIDI CH: 10 (canal de percusión General MIDI)
    NOTE: C3  (nota 36 = Kick)
    VELOCITY: VARIABLE (V VELO activado)
  → Repite para cada pad:
    Pad 2 → D3 (38 = Snare)
    Pad 3 → F#3 (42 = Hi-Hat cerrado)
    Pad 4 → A#3 (46 = Hi-Hat abierto)
    Pad 5 → C4 (48 = Tom bajo)
    Pad 6 → E4 (52 = Tom medio)
    Pad 7 → A4 (57 = Crash)
    Pad 8 → D4 (50 = Tom alto)

PASO 2: En FL Studio:
  → Channel Rack → Add one → FPC
  → FPC recibe en Canal 10 por defecto
  → Arrastra tus samples de batería a los pads del FPC
  → Los pads del MOTOR 61 activan los pads del FPC
```

### Banco 2 de Pads — Sonidos Alternativos

```
En MOTOR 61: selecciona [PAD BANK] "9-16"
→ Asigna notas diferentes (para samples alternativos o percusión adicional)
→ Guarda en el mismo preset

En FL Studio:
→ Crea otro instrumento de batería (FPC 2 o un sampler)
→ Asígnalo al mismo canal MIDI 10 pero con notas diferentes
→ Cambia con [PAD BANK] durante la actuación
```

### Colores de Pads para Identificación Visual

```
[GLOBAL] → PADS → COLOR → selecciona cada pad → elige color

Sugerencia de código de colores:
🔴 Rojo → Kick (Pad 1)
🟡 Amarillo → Snare (Pad 2)
🔵 Azul → Hi-Hats (Pads 3-4)
🟢 Verde → Toms (Pads 5-6-8)
⚪ Blanco → Platillos (Pad 7)
```

---

## 7. Usar Program Change para Cambiar Instrumentos

El MOTOR 61 puede enviar **Program Change** desde los pads para cambiar de preset en un instrumento o plugin de FL Studio.

### Configuración del Menú P.CHNG

```
Presiona [P CHNG] en el MOTOR 61

OPCIÓN 1 — PAD ASSIGN (asignación permanente por pad):
  → Selecciona el pad
  → MIDI OUT: USB+MIDI
  → MIDI CHAN: 1 (o el canal del instrumento en FL)
  → TYPE: PGM CHNG
  → NUMBER: 0-127 (número del preset/programa)
  → FIX/INC/DEC: FIX (número fijo) o INC/DEC (paso a paso)
  → Presiona [P CHNG] y luego el pad para enviarlo

OPCIÓN 2 — SINGLE SEND (envío único personalizado):
  → Configura número, canal, tipo
  → Presiona DATA para confirmar y enviar inmediatamente
```

### Uso en FL Studio con VSTi que Soporte Program Change

```
En el plugin (ej. un sintetizador VSTi):
→ Debe tener "Receive MIDI program change" activado en sus opciones
→ Cada Program Change cambiará el preset del plugin
→ Útil para baterías que tienen múltiples kits (kits 1-128)
```

---

## 8. MIDI Learn en Plugins de FL Studio

FL Studio tiene una función **MIDI Learn** que permite mapear cualquier CC o movimiento del MOTOR 61 a cualquier parámetro de un plugin:

### Procedimiento de MIDI Learn

```
1. Abre el plugin en FL Studio (sintetizador, efecto, etc.)

2. Clic derecho en el parámetro que quieres controlar
   (ej. clic derecho sobre el knob "Filter Cutoff")
   → Aparece el menú contextual

3. Selecciona: "Link to controller..."
   → Se abre el diálogo de vinculación MIDI

4. En el MOTOR 61:
   → Mueve el control físico que quieres asignar
   (ej. Encoder 1, o Fader 3)
   → FL Studio detecta automáticamente el CC y el canal

5. Clic en "Accept"
   → El encoder/fader del MOTOR 61 ahora controla ese parámetro

6. Para ver todos los vínculos activos:
   → Tools → Last tweaked (historial de mappings)
```

### Mapeo Masivo con el Asistente de FL Studio

Para mapear todos los faders/encoders de una vez:

```
Options → MIDI Settings → selecciona el MOTOR61 → "Configure..."
→ Mueve cada control del MOTOR 61
→ FL Studio los registra en orden
→ Asígnalos a parámetros específicos del proyecto
→ Guarda la configuración como preset del controlador
```

---

## 9. Guardar el Mapeo como Proyecto Template

Para no repetir la configuración cada vez que abres FL Studio:

### Guardar como Plantilla de Proyecto

```
1. Configura el proyecto con todos los instrumentos y mapeos del MOTOR 61

2. File → Save as → guarda en:
   %USERPROFILE%\Documents\Image-Line\FL Studio\Projects\Templates\

3. Ponle un nombre descriptivo: "MOTOR61_Template.flp"

4. La próxima vez: File → New from template → MOTOR61_Template

Qué incluye la plantilla:
✅ Canales del Channel Rack con instrumentos
✅ Configuración de canales MIDI por instrumento
✅ MIDI Learn mappings de CC a parámetros
✅ Layout del Mixer
✅ Rutas de audio configuradas
```

### Guardar Configuración del Controlador (Controller Preset)

```
Options → MIDI Settings → MOTOR61 → botón "Save" o "Save preset"
→ Nombre: "MOTOR61_Studio" o "MOTOR61_Live"
→ Se guarda en: %USERPROFILE%\Documents\Image-Line\FL Studio\Settings\Hardware\
```

---

## 10. Referencia de Notas MIDI

### Numeración de Notas (convención FL Studio)

FL Studio usa la convención donde **C5 = nota MIDI 60 (Middle C)**:

```
┌──────┬──────┬──────┬──────┬──────┬──────┬──────┬──────┬──────┐
│ C0   │ C1   │ C2   │ C3   │ C4   │ C5   │ C6   │ C7   │ C8   │
│  0   │  12  │  24  │  36  │  48  │  60  │  72  │  84  │  96  │
│      │      │      │      │      │ (MC) │      │      │      │
└──────┴──────┴──────┴──────┴──────┴──────┴──────┴──────┴──────┘
```

> **Nota:** Algunas fuentes y plugins usan C4 = 60 (Middle C). Si un sonido no suena  
> en la nota esperada, prueba desplazando una octava arriba o abajo con los botones  
> [OCTAVE] del MOTOR 61.

### Rango del Teclado del MOTOR 61

```
MOTOR 61: 61 teclas → desde C2 hasta C7 (en posición Octave 0)

Con los botones OCTAVE ±:
  Octave +3 → C5 hasta C10
  Octave -3 → C-1 hasta C4

Presionar ambos OCTAVE al mismo tiempo → resetea a Octave 0
```

---

> **Ver también:**
> - [ASIGNACION_NOTAS_CC.md](ASIGNACION_NOTAS_CC.md) — Asignaciones en el hardware del MOTOR 61
> - [PERFORMANCE_EN_VIVO.md](PERFORMANCE_EN_VIVO.md) — Mapeo práctico para performances en vivo
> - [PRESETS_GUIA.md](PRESETS_GUIA.md) — Guardar configuraciones de mapeo en presets
