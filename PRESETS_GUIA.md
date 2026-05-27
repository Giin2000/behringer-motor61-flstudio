# 💾 Guía de Presets — Behringer MOTOR 61

> **← Volver al [README](README.md)**  
> Basado en el **Capítulo 10** del manual oficial del MOTOR 61/49.

---

## Índice

1. [Qué es un Preset](#1-qué-es-un-preset)
2. [Estructura de Memoria](#2-estructura-de-memoria)
3. [Cargar un Preset (Carga Rápida)](#3-cargar-un-preset-carga-rápida)
4. [Menú EDIT → PRESETS](#4-menú-edit--presets)
5. [Guardar el Primer Preset](#5-guardar-el-primer-preset)
6. [Actualizar un Preset Existente](#6-actualizar-un-preset-existente)
7. [Renombrar un Preset](#7-renombrar-un-preset)
8. [Eliminar un Preset](#8-eliminar-un-preset)
9. [Vista General de Presets](#9-vista-general-de-presets)
10. [Exportar Presets por SysEx](#10-exportar-presets-por-sysex)
11. [Restaurar Configuración de Fábrica](#11-restaurar-configuración-de-fábrica)
12. [Flujo de Trabajo Recomendado](#12-flujo-de-trabajo-recomendado)

---

## 1. Qué es un Preset

Un **preset** del MOTOR 61 guarda la configuración interna del teclado:

```
✅ Lo que SÍ guarda un preset:
├── Asignaciones de CC y Notas (faders, encoders, pads, botones, pedales)
├── Canal MIDI global y por control
├── Modo de transporte (MMC, MIDI, MIDI Control, etc.)
├── Configuración del arpeggiador (estilo, gate, rango, swing, split)
├── Colores de los pads (16 opciones por pad)
├── Sensibilidad de velocidad del teclado y los pads
├── Configuración de aftertouch
├── Valores de inicio y fin de CC
└── Modo de LED rings de los encoders

❌ Lo que NO guarda un preset:
├── Configuraciones de FL Studio o cualquier DAW
├── Mapeos de teclas en el software
└── Ajustes de brillo/contraste del display (son globales, no de preset)
```

> **Nota importante:** Los presets del MOTOR 61 son independientes de los presets de tu DAW.  
> Para guardar la configuración de FL Studio, usa las herramientas de guardado del propio FL Studio.

---

## 2. Estructura de Memoria

```
┌─────────────────────────────────────────────────────┐
│           MEMORIA DE PRESETS DEL MOTOR 61            │
├──────────────────────────────────────────────────────┤
│  PRESET 0 — DEFAULT (fábrica)                        │
│  ├── No se puede borrar                              │
│  ├── No se puede renombrar                           │
│  ├── No se puede sobreescribir                       │
│  └── Siempre disponible como punto de retorno        │
├──────────────────────────────────────────────────────┤
│  PRESET 1  → PRESET 64  (usuario)                    │
│  ├── 64 espacios de memoria de usuario               │
│  ├── Inicialmente todos en estado "EMPTY"            │
│  ├── Cada uno puede tener nombre de hasta 10 chars   │
│  └── Pueden guardarse, renombrarse, copiarse y       │
│       borrarse libremente                            │
└──────────────────────────────────────────────────────┘
```

> **Advertencia de firmware:** Actualizar el firmware del MOTOR 61 **borrará todos tus presets de usuario**.  
> Exporta tus presets por SysEx antes de actualizar (ver sección 10).

---

## 3. Cargar un Preset (Carga Rápida)

Este es el método más rápido para cambiar de preset durante el uso normal.

### Procedimiento

```
1. Presiona el botón [PRESET]
   → El display muestra el preset actual (número y nombre)

2. Presiona el encoder [DATA] (empujar, no girar)
   → El display entra en modo de selección

3. Gira el encoder [DATA]
   → Desplaza entre todos los presets guardados (no vacíos)
   → Solo aparecen presets que tienen datos guardados

4. Al encontrar el preset deseado, presiona [DATA] nuevamente
   → El preset se carga inmediatamente
```

### Notas sobre la Carga Rápida

- Solo muestra presets **no vacíos** (los espacios EMPTY no aparecen)
- Si no has creado ningún preset, solo aparece el **DEFAULT (Preset 0)**
- La carga es instantánea: todos los parámetros cambian al presionar DATA

---

## 4. Menú EDIT → PRESETS

Para todas las operaciones avanzadas (guardar, copiar, borrar, renombrar):

```
Presiona [EDIT] → Gira DATA hasta "1. PRESETS" → Presiona DATA
```

Esto accede al menú principal de gestión de presets con 5 opciones:

| # | Opción | Función |
|---|---|---|
| 1 | **SAVE/COPY PRESET** | Guardar preset actual o copiar a otra posición |
| 2 | **DELETE PRESET** | Borrar un preset (no borra el DEFAULT) |
| 3 | **RENAME PRESET** | Cambiar el nombre de un preset existente |
| 4 | **PRESET OVERVIEW** | Lista completa de las 64 posiciones de memoria |
| 5 | **SYSEX TX** | Exportar preset(s) por USB como SysEx MIDI |

---

## 5. Guardar el Primer Preset

Cuando el teclado es nuevo, solo existe el **DEFAULT (Preset 0)**. Para crear tu primer preset de usuario:

### Paso a Paso

```
SITUACIÓN: Has modificado parámetros del teclado (colores, CC, etc.)
y quieres guardar esa configuración como Preset 1.

1. Presiona [EDIT]
   → Display: menú EDIT

2. Gira DATA → selecciona "1. PRESETS" → Presiona DATA
   → Display: menú PRESETS

3. Gira DATA → selecciona "1. SAVE/COPY PRESET" → Presiona DATA
   → Display: muestra "SOURCE: PRESET 0 (DEFAULT)"

4. Presiona DATA para confirmar el DEFAULT como fuente (SOURCE)
   → Display: muestra "DESTINATION:"

5. Gira DATA para seleccionar el número de destino (ej. PRESET 1)
   → Display: "PRESET 1" (en este ejemplo)

6. Presiona DATA para confirmar
   → Display: "COPY PRESET?" (si el destino está vacío)
               "OVERWRITE?" (si el destino ya tiene un preset)

7. Gira DATA → selecciona "YES" → Presiona DATA
   → Display: "SUCCESS!"

8. Tu configuración está guardada en PRESET 1 con el nombre "DEFAULT"
   → Ahora ve a RENAME PRESET para cambiarle el nombre (sección 7)
```

---

## 6. Actualizar un Preset Existente

Si cargaste un preset, hiciste modificaciones y quieres **guardar los cambios** sobreescribiendo el original:

```
SITUACIÓN: Tienes el PRESET 9 cargado y has modificado parámetros.
Quieres actualizar ese mismo preset con los nuevos cambios.

1. [EDIT] → DATA → "1. PRESETS" → DATA
   → Estás en el menú PRESETS

2. DATA → "1. SAVE/COPY PRESET" → DATA
   → Display: lista de presets SOURCE

3. Gira DATA → selecciona el número de tu preset actual (ej. PRESET 9)
   → Presiona DATA para confirmar como SOURCE

4. Gira DATA → selecciona el MISMO número como DESTINATION (ej. PRESET 9)
   → Presiona DATA para confirmar

5. Display: "OVERWRITE?"
   → Gira DATA → selecciona "YES" → Presiona DATA

6. Display: "SUCCESS!"
   → El preset 9 ha sido actualizado con tus nuevos ajustes
```

> **Tip:** Si quieres conservar el original Y tener la versión modificada,  
> elige un número de destino diferente en el paso 4 y luego renombra el nuevo preset.

---

## 7. Renombrar un Preset

Los presets guardados se llaman "DEFAULT" por defecto. Renombrarlos es esencial para organizarse.

### Procedimiento de Renombrado

```
1. [EDIT] → DATA → "1. PRESETS" → DATA

2. Gira DATA → selecciona "3. RENAME PRESET" → Presiona DATA

3. Gira DATA para navegar entre presets → encuentra el que quieres renombrar
   → Presiona DATA para seleccionarlo
   (Los presets EMPTY no pueden renombrarse)

4. El display muestra el nombre actual con la PRIMERA letra resaltada
   (Ej: "D" en "DEFAULT")

5. Gira DATA → selecciona el nuevo carácter para esa posición
   (Ej: la "S" de "STUDIO")

6. Presiona DATA para confirmar ese carácter y avanzar al siguiente

7. Repite los pasos 5-6 para cada carácter del nombre

8. ⚠️ IMPORTANTE: Presiona [FWD] para GUARDAR el nuevo nombre
   Si no presionas FWD, el nombre NO se cambiará

9. Display: "SUCCESS!" — El preset tiene su nuevo nombre
```

### Caracteres Disponibles para Nombres

```
Espacio en blanco (girar DATA muy rápido en sentido antihorario)
! " # $ % & ' ( ) * + , - . /
0 1 2 3 4 5 6 7 8 9
: ; < = > ?
A B C D E F G H I J K L M N O P Q R S T U V W X Y Z

Longitud máxima: 10 caracteres
Para llegar a "Z": girar DATA muy rápido en sentido horario
```

### Ejemplos de Nombres Útiles

| Uso del Preset | Nombre sugerido |
|---|---|
| Mezcla de estudio | `STUDIO MX` |
| Performance en vivo | `LIVE SET1` |
| Batería + pads | `DRUMS PAD` |
| Sintetizador lead | `SYNTH LD` |
| Producción de beats | `BEAT PROD` |
| Preset de Arp activo | `ARP LIVE` |

---

## 8. Eliminar un Preset

```
1. [EDIT] → DATA → "1. PRESETS" → DATA

2. Gira DATA → selecciona "2. DELETE PRESET" → Presiona DATA

3. Gira DATA para navegar → encuentra el preset a borrar
   → Presiona DATA para seleccionarlo
   (El DEFAULT PRESET 0 no aparece — no puede borrarse)

4. El display muestra una pantalla de verificación
   → Presiona DATA para confirmar el borrado

5. Display: "DELETING..." → "DELETE OK"
   → El espacio de memoria vuelve a estado "EMPTY"
```

> **Precaución:** El borrado no tiene deshacer. Si quieres conservar una copia,  
> usa SYSEX TX para exportarlo antes de borrar (ver sección 10).

---

## 9. Vista General de Presets

El **Preset Overview** es la vista de lista completa de las 64 posiciones:

```
1. [EDIT] → DATA → "1. PRESETS" → DATA

2. Gira DATA → selecciona "4. PRESET OVERVIEW" → Presiona DATA

3. El display muestra 8 presets a la vez en formato de lista:
   ┌──────────────────────────┐
   │  [1] STUDIO MX           │  ← Preset actualmente cargado (número resaltado)
   │   2  LIVE SET1           │
   │   3  DRUMS PAD           │
   │   4  SYNTH LD ◄──────── │  ← Preset seleccionado para cargar (nombre resaltado)
   │   5  EMPTY               │
   │   6  EMPTY               │
   │   7  ARP LIVE            │
   │   8  BEAT PROD           │
   └──────────────────────────┘

4. Gira DATA para desplazarte por los 64 slots

5. Presiona DATA sobre un preset (no vacío) para cargarlo
   → Display: "LOADING..." → confirmación
   (Los presets EMPTY no pueden cargarse desde aquí)
```

---

## 10. Exportar Presets por SysEx

Permite hacer **backup** de tus presets enviándolos a tu ordenador via MIDI SysEx:

```
1. [EDIT] → DATA → "1. PRESETS" → DATA

2. Gira DATA → selecciona "5. SYSEX TX" → Presiona DATA

3. El display ofrece dos opciones:
   ├── ALL PRESETS → exporta los 64 presets a la vez
   └── SINGLE PRESET → exporta solo el preset seleccionado

4. Gira DATA → elige YES → Presiona DATA
   → Los datos SysEx se envían por USB a tu ordenador

Recepción en el ordenador:
  ├── FL Studio → MIDI settings → habilita la entrada del MOTOR 61
  │   (captura SysEx automáticamente si está activo)
  └── Recomendado: usar un capturador SysEx dedicado
      (MIDI-OX en Windows, SysEx Librarian en macOS)
```

> **Cuándo usar esto:**
> - Antes de actualizar el firmware (que borra todos los presets)
> - Para compartir presets entre equipos
> - Como backup antes de un evento en vivo

---

## 11. Restaurar Configuración de Fábrica

```
⚠️ ADVERTENCIA: Esta operación borra TODOS los presets de usuario
y restablece TODOS los ajustes globales a sus valores de fábrica.
No hay forma de deshacer este proceso.

Ruta: GLOBAL → DEVICE → RESET SETTINGS → confirmar con YES

Resultado:
├── Todos los Presets 1-64: borrados (quedan como EMPTY)
├── DEFAULT Preset 0: restaurado a valores de fábrica
├── Todos los ajustes GLOBAL: valores por defecto
└── Colores de pads, asignaciones CC, etc.: reseteados
```

---

## 12. Flujo de Trabajo Recomendado

### Para Producción en Estudio

```
Sesión nueva
    ↓
Cargar preset adecuado [PRESET] → DATA → girar → DATA
    ↓
Producir / ajustar parámetros según necesidad
    ↓
¿Quieres guardar cambios?
    ├── SÍ, mismo preset → EDIT → SAVE/COPY → source = dest (OVERWRITE)
    └── SÍ, preset nuevo → EDIT → SAVE/COPY → nuevo número → RENAME
    ↓
Exportar backup si hiciste cambios importantes → SYSEX TX
```

### Para Performance en Vivo

```
Antes del evento:
1. Crea un preset por canción o sección del set
2. Nómbralos claramente: "INTRO", "VERSO1", "CORO", etc.
3. Asígnales números consecutivos (ej. 1-10 para un set de 10 temas)
4. Haz backup SysEx
5. Practica el cambio de presets con [PRESET] → DATA → DATA

Durante el show:
→ Cambio rápido: [PRESET] → DATA encoder (una vuelta) → DATA
→ Tiempo estimado de cambio: 2-3 segundos
→ El cambio es silencioso (no envía notas indeseadas)
```

---

> **Ver también:**
> - [ASIGNACION_NOTAS_CC.md](ASIGNACION_NOTAS_CC.md) — Cómo personalizar CC y Notas antes de guardar el preset
> - [PERFORMANCE_EN_VIVO.md](PERFORMANCE_EN_VIVO.md) — Estrategias de presets para presentaciones
