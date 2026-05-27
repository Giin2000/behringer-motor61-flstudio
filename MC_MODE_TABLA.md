# 🎛️ Tabla de Funciones — Modo Mackie Control (MC Mode)

> **← Volver al [README](README.md)**

---

## ¿Qué es el Mackie Control Mode?

El **Mackie Control Universal (MCU)** es un protocolo de control de superficies MIDI ampliamente adoptado por los principales DAWs (FL Studio, Ableton, Logic, Cubase, Pro Tools). Permite que el hardware controle el software mediante mensajes MIDI estandarizados, con comunicación **bidireccional**: el hardware controla el software Y el software actualiza el hardware (mueve faders, enciende LEDs, actualiza displays).

El Behringer MOTOR 61 implementa este protocolo en su **Puerto 2 (MIDIIN2/MIDIOUT2)**.

---

## 🔑 Regla Fundamental

```
╔══════════════════════════════════════════════════════╗
║  MC MODE debe estar SIEMPRE ACTIVO                   ║
║                                                      ║
║  Sin MC Mode:                                        ║
║  ├── MIDIIN2/MIDIOUT2 pueden no aparecer             ║
║  ├── Los mensajes MC no se generan                   ║
║  ├── Faders, botones y LEDs no responden             ║
║  └── FL Studio no puede comunicarse con el hardware  ║
╚══════════════════════════════════════════════════════╝
```

---

## Activación del MC Mode

### Método General

```
┌─────────────────────────────────────────┐
│  ENCENDER el MOTOR 61                   │
│           ↓                             │
│  Mantener [SETUP]                       │
│           ↓                             │
│  Presionar botón MC / CTRL              │
│  (mientras se mantiene SETUP)           │
│           ↓                             │
│  Display muestra: "MC" o "MACKIE"       │
│           ↓                             │
│  Soltar ambos botones                   │
│           ↓                             │
│  Guardar: [SETUP] 3s o [STORE]          │
└─────────────────────────────────────────┘
```

### Indicadores de MC Mode Activo

| Indicador | Qué observar |
|---|---|
| Display LCD | Muestra "MC", "MCU" o "MACKIE" |
| LED de modo | Indicador MC iluminado (si existe) |
| Comportamiento de faders | Ligera resistencia por los motores activos |
| Puerto MIDI | MIDIIN2 y MIDIOUT2 visibles en el sistema |

---

## Tabla Completa de Funciones en MC Mode

### Sección de Transporte

| Botón MOTOR 61 | Mensaje MC | Función en FL Studio |
|---|---|---|
| `PLAY` ▶ | `0x5E` | Iniciar reproducción |
| `STOP` ■ | `0x5D` | Detener reproducción |
| `REC` ● | `0x5F` | Activar/desactivar grabación |
| `REWIND` ◀◀ | `0x5B` | Rebobinar / Ir al inicio |
| `FAST FWD` ▶▶ | `0x5C` | Avance rápido |
| `LOOP` ↺ | `0x56` | Activar/desactivar bucle |
| `PUNCH` | `0x55` | Punch in/out |

---

### Sección de Faders (Canales 1-8 + Master)

| Control | Mensaje MC | Rango | Función en FL Studio |
|---|---|---|---|
| Fader canal 1-8 | Pitch Bend CH 1-8 | 0–16383 | Volumen del canal del mixer (0–100%) |
| Fader Master | Pitch Bend CH 9 | 0–16383 | Volumen master del mixer |
| Tocar fader | `0x68`–`0x6F` | On/Off | Touch sensing — activa/desactiva escritura de automatización |

---

### Encoders Rotativos (V-Pot / Knobs)

| Control | Mensaje MC | Función predeterminada en FL Studio |
|---|---|---|
| Encoder 1-8 (giro) | CC 16-23 | Pan (paneo) del canal correspondiente |
| Encoder 1-8 (presionar) | `0x20`–`0x27` | Reset pan al centro / función alternativa |
| Encoder de navegación | CC 60 (Jog Wheel) | Desplazamiento de la línea de tiempo |

---

### Botones de Selección de Canal

| Botón | Mensaje MC | Función en FL Studio |
|---|---|---|
| `SELECT 1-8` | `0x18`–`0x1F` | Seleccionar canal de mixer activo |
| `MUTE 1-8` | `0x10`–`0x17` | Silenciar/activar canal |
| `SOLO 1-8` | `0x08`–`0x0F` | Solo del canal (silencia los demás) |
| `REC/ARM 1-8` | `0x00`–`0x07` | Armar canal para grabación |

---

### Botones de Navegación de Banco

| Botón | Mensaje MC | Función |
|---|---|---|
| `BANK LEFT` / `<<` | `0x2E` | Retroceder 8 canales (banco anterior) |
| `BANK RIGHT` / `>>` | `0x2F` | Avanzar 8 canales (banco siguiente) |
| `CHANNEL LEFT` / `<` | `0x30` | Retroceder 1 canal |
| `CHANNEL RIGHT` / `>` | `0x31` | Avanzar 1 canal |

---

### Botones de Modo de Encoder (Assign)

| Botón | Función |
|---|---|
| `PAN` | Encoders controlan paneo de canales |
| `SEND` | Encoders controlan nivel de sends/efectos |
| `EQ` | Encoders controlan bandas de EQ (si disponible) |
| `PLUGIN` | Encoders controlan parámetros del plugin activo |
| `TRACK` | Encoders controlan parámetros del track |
| `INSTRUMENT` | Encoders controlan parámetros del instrumento |

---

### Display LCD — Información Enviada por FL Studio

```
┌──────────────────────────────────────┐
│  CH1   CH2   CH3   CH4   CH5  ...    │  ← Nombre de canal (hasta 6 caracteres)
│  Vol   Pan   Send  EQ    ...         │  ← Parámetro activo
│  0.0dB -3.2  +5.1  100%  ...         │  ← Valor actual
└──────────────────────────────────────┘
```

FL Studio envía estos datos a través de **MIDIOUT2** (SysEx Mackie). Sin MIDIOUT2 configurado, el display permanece vacío o muestra datos por defecto.

---

### Mensajes de Retorno (FL Studio → MOTOR 61)

Estos mensajes los envía FL Studio al MOTOR 61 para actualizar el hardware:

| Tipo de Mensaje | Descripción |
|---|---|
| `Pitch Bend` CH 1-9 | Actualiza posición de faders motorizados |
| `SysEx Mackie` | Actualiza texto en el display LCD |
| `Note On/Off` | Controla los LEDs de los botones |
| `CC 0x0C` | Indica actividad de VU meters |

---

## Comparación: MC Mode vs. Modo Normal

| Función | MC Mode | Modo Normal (sin MC) |
|---|---|---|
| Faders motorizados | ✅ Controlados por DAW | ❌ Solo físicos, sin feedback |
| Display LCD | ✅ Muestra datos del DAW | ❌ Datos genéricos o vacío |
| Botones con LED | ✅ LEDs reflejan estado del DAW | ❌ Comportamiento manual |
| MIDIIN2/MIDIOUT2 | ✅ Disponibles | ❌ Solo Puerto 1 visible |
| Integración total con FL | ✅ Completa | ❌ Solo MIDI básico |
| Notas de teclado | ✅ Puerto 1 sigue activo | ✅ Puerto 1 activo |

---

## Estructura Técnica del Protocolo MC

```
MOTOR 61 Hardware
│
├── Puerto 1 (MIDIIN / MIDIOUT)
│   └── MIDI estándar: notas, CC, pitch bend, aftertouch
│       → Instrumentos virtuales, grabación de notas
│
└── Puerto 2 (MIDIIN2 / MIDIOUT2) [REQUIERE MC MODE ACTIVO]
    ├── MIDIIN2 → FL Studio: recibe comandos del hardware
    │   ├── Fader movements (Pitch Bend por canal)
    │   ├── Button presses (Note On/Off con notas específicas MC)
    │   └── Encoder rotations (CC values)
    │
    └── MIDIOUT2 → MOTOR 61: FL Studio actualiza el hardware
        ├── Fader positions (mueve los motores)
        ├── LED states (ilumina botones)
        ├── Display text (SysEx con nombres de canales)
        └── VU meter data (actividad de nivel)
```

---

## Mensajes MIDI Clave del Protocolo Mackie Control

Para usuarios avanzados que quieran depurar o crear scripts personalizados:

```
Nota: Todos los botones MC usan Note On (velocidad 127 = presionado, 0 = soltado)
      Los faders usan Pitch Bend en cada canal MIDI (canal 1-9)
      Los encoders usan Control Change (CC) en valores relativos
```

| Función | Tipo MIDI | Canal | Nota/CC | Valor |
|---|---|---|---|---|
| PLAY | Note On/Off | 1 | 94 (0x5E) | 127/0 |
| STOP | Note On/Off | 1 | 93 (0x5D) | 127/0 |
| REC | Note On/Off | 1 | 95 (0x5F) | 127/0 |
| Fader canal 1 | Pitch Bend | 1 | — | 0–16383 |
| Fader canal 2 | Pitch Bend | 2 | — | 0–16383 |
| Fader master | Pitch Bend | 9 | — | 0–16383 |
| Select canal 1 | Note On/Off | 1 | 24 (0x18) | 127/0 |
| Mute canal 1 | Note On/Off | 1 | 16 (0x10) | 127/0 |
| Solo canal 1 | Note On/Off | 1 | 8 (0x08) | 127/0 |
| Pan encoder 1 | CC | 1 | 16 (0x10) | 1-127 (relativo) |

---

> **Referencia oficial del protocolo MCU:**  
> Mackie Control Universal Protocol — Mackie Designs Inc.  
> Muchos DAWs lo implementan con ligeras variaciones; FL Studio sigue la especificación estándar.

---

> Para problemas relacionados con MC Mode, ver [PROBLEMAS_COMUNES.md](PROBLEMAS_COMUNES.md)  
> Para la configuración en FL Studio, ver [CONFIGURACION_FL_STUDIO.md](CONFIGURACION_FL_STUDIO.md)
