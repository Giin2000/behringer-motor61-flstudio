# 🎤 Performance en Vivo con MOTOR 61 + FL Studio 20+

> **← Volver al [README](README.md)**

---

## Índice

1. [Filosofía del Set en Vivo](#1-filosofía-del-set-en-vivo)
2. [Configuración Hardware para Directo](#2-configuración-hardware-para-directo)
3. [Los 8 Pads para Batería en Vivo](#3-los-8-pads-para-batería-en-vivo)
4. [Arpeggiador en Tiempo Real](#4-arpeggiador-en-tiempo-real)
5. [Botones de Transporte para Control del Set](#5-botones-de-transporte-para-control-del-set)
6. [Cambio de Presets en Vivo](#6-cambio-de-presets-en-vivo)
7. [Estrategias de Faders para el Directo](#7-estrategias-de-faders-para-el-directo)
8. [Tips para Actuaciones Estables](#8-tips-para-actuaciones-estables)
9. [Checklist Pre-Show](#9-checklist-pre-show)
10. [Recuperación de Errores en Vivo](#10-recuperación-de-errores-en-vivo)

---

## 1. Filosofía del Set en Vivo

### Modo de Operación Recomendado: MC Mode Permanente

Tal como describe el manual oficial del MOTOR 61:

> *"When using the MOT�R in MC mode, it is not recommended to toggle between MIDI  
> and MC mode when you switch from song-mixing to instrument-playing and vice versa.  
> Please keep MC mode active."*

```
REGLA DE ORO PARA DIRECTO:
╔══════════════════════════════════════════════════════════════╗
║  Mantén MC MODE ACTIVO durante TODO el set                   ║
║                                                              ║
║  ✅ MC Mode activo = Rendimiento híbrido simultáneo:         ║
║     • Teclado y pads → MIDI normal (Puerto 1)                ║
║     • Faders, encoders, transporte → Mackie Control (Puerto 2)║
║                                                              ║
║  ❌ No alternar entre MIDI y MC mode durante una actuación    ║
║     Causa desorientación del hardware y pérdida de sync      ║
╚══════════════════════════════════════════════════════════════╝
```

### Ventaja del Modo Híbrido del MOTOR 61

La arquitectura de doble puerto del MOTOR 61 es ideal para directo porque **no requiere elegir entre tocar y controlar**:

```
Mientras tocas el teclado (Puerto 1):
  → Notas en tus instrumentos virtuales
  → Pads para batería
  → Ruedas de pitch y modulación

Al mismo tiempo (Puerto 2):
  → Faders controlan volúmenes del mixer de FL Studio
  → Botones de transporte arrancan/paran el set
  → Encoders ajustan parámetros en tiempo real
```

---

## 2. Configuración Hardware para Directo

### Setup Físico Recomendado

```
╔═══════════════════════════════════════════════════════════╗
║                  SETUP DE DIRECTO                          ║
║                                                            ║
║  [Adaptador 12V] ──── [MOTOR 61] ──── [USB] ──── [Laptop] ║
║                            │                       │       ║
║                     [Pedal Sustain]           [Interfaz]   ║
║                     [Pedal Expresión]         de Audio     ║
║                                                    │       ║
║                                               [PA / Mesa]  ║
╚═══════════════════════════════════════════════════════════╝

Checklist de conexiones:
☐ Adaptador 12V conectado (CRÍTICO para motores)
☐ Cable USB al laptop (usar cable corto y de calidad)
☐ Pedal de sustain conectado
☐ Pedal de expresión conectado (opcional pero recomendado)
☐ Audio de FL Studio → Interfaz audio → PA/monitores
☐ MC Mode activo en el MOTOR 61
```

### Consideraciones del Laptop para Directo

```
Antes del show, en el laptop:
☐ Modo de ahorro de energía: DESACTIVADO (alto rendimiento)
☐ Wifi: DESACTIVADO
☐ Notificaciones del sistema: DESACTIVADAS
☐ Actualizaciones automáticas: DESACTIVADAS (especialmente Windows Update)
☐ Protector de pantalla: DESACTIVADO
☐ Suspensión automática: DESACTIVADA
☐ Buffer de audio de FL Studio: aumentar si hay cortes (ej. 512 o 1024 samples)
☐ Proyecto guardado y cargado (no trabajar sobre proyectos sin guardar)
```

---

## 3. Los 8 Pads para Batería en Vivo

### Configuración Base de los Pads

Los pads del MOTOR 61 tienen:
- **Sensibilidad de velocidad:** variable (V VELO) o fija (F VELO)
- **Aftertouch:** presión continua después del impacto (configurar sensibilidad o desactivar)
- **4 bancos:** 32 "pads virtuales" con asignaciones independientes
- **Note Repeat:** re-trigger automático manteniendo el pad presionado
- **Double Beat:** envía nota al presionar Y al soltar (simula bombo doble)

### Configuración de Velocidad Óptima para Directo

```
[GLOBAL] → PADS → PAD VELOCITY → selecciona según tu técnica:
  SOFT   → para toques suaves, respuesta más fácil
  MEDIUM → equilibrio entre sensibilidad y control (recomendado)
  HARD   → requiere más fuerza, menos notas accidentales en directo

[GLOBAL] → PADS → FIXED VELOCITY → (si usas F VELO)
  → Valor entre 90-110 para batería en vivo: consistente y contundente

[GLOBAL] → PADS → AFTER TOUCH SENSITIVITY → OFF
  → Para batería en directo: DESACTIVAR el aftertouch (reduce MIDI innecesario)
```

### Asignación de 4 Bancos de Pads para un Set Completo

```
PAD BANK 1-8: Kit de batería principal
┌─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┐
│ KCK │ SNR │ HH. │ HHo │ TL  │ TM  │ TH  │ CRS │
│ C3  │ D3  │ F#3 │ A#3 │ C4  │ E4  │ D4  │ A4  │
└─────┴─────┴─────┴─────┴─────┴─────┴─────┴─────┘

PAD BANK 9-16: Percusión adicional / samples de impacto
┌─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┐
│CLAP │TAMB │COWB │SHAK │FX1  │FX2  │RYDE │OPEN │
└─────┴─────┴─────┴─────┴─────┴─────┴─────┴─────┘

PAD BANK 17-24: Samples de loops o one-shots
┌─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┐
│LOP1 │LOP2 │LOP3 │LOP4 │HIT1 │HIT2 │HIT3 │HIT4 │
└─────┴─────┴─────┴─────┴─────┴─────┴─────┴─────┘

PAD BANK 25-32: Program Change / cambio de escenas
└─ Ver sección 6 (Cambio de Presets en Vivo)
```

### Note Repeat para Rollos y Fills

```
Botón [REPEAT] activa el modo de re-trigger continuo:
→ Mantén un pad presionado → se re-dispara automáticamente

Controlar la velocidad del repeat:
→ [TIME DIVISION] <<< / >>> : cambia entre 1/4, 1/8, 1/16, 1/32T, etc.
→ [TEMPO] (tap): ajusta el BPM del arpeggiador/repeat

Configurar el gate del repeat:
→ [EDIT] → PAD NOTE REPEAT → GATE → (valor musical)
→ Valores largos = notas sostenidas y fusionadas
→ Valores cortos = "machine gun" staccato

Swing en el repeat:
→ [EDIT] → PAD NOTE REPEAT → SWING → añade groove al repeat
```

### Double Beat (Bombo Doble)

```
Botón [D BEAT] activa el doble disparo:
→ Nota ON al PRESIONAR el pad
→ Nota ON al SOLTAR el pad
→ Simula un bombo doble sin necesitar dos pads

Ideal para:
  → Kick de bombo doble veloz
  → Doubles en snare con un solo dedo
```

---

## 4. Arpeggiador en Tiempo Real

### Activar y Configurar el Arpeggiador

```
Botón [ARPEG] → activa/desactiva el arpeggiador del MOTOR 61
Botón [A LATCH] → latch: el arpeggio continúa después de soltar las teclas
```

### Estilos de Arpeggio

Configura el estilo en: `[EDIT] → ARPEGGIATOR → 1. STYLE`

| Estilo | Patrón | Uso en vivo |
|---|---|---|
| **UP** | Notas de grave a agudo | Líneas melódicas ascendentes |
| **DOWN** | Notas de agudo a grave | Líneas descendentes, efecto "falling" |
| **ORDER** | En el orden que presionas | Control total del orden — más musical |
| **INCLUDE** | Grave → agudo → grave (con notas extremas repetidas) | Patrón continuo suave |
| **EXCLUDE** | Grave → agudo → grave (sin repetir extremos) | Más limpio, sin doble disparo |
| **RANDOM** | Orden aleatorio | Texturas generativas, impredecible |
| **CHORD** | Todas las notas simultáneas, rítmico | Comping de acordes rítmico |

### Parámetros de Temporización

```
[EDIT] → ARPEGGIATOR

2. GATE (duración de nota):
   → Valores cortos (1/32): notas staccato muy rápidas
   → Valores medios (1/8): articulación normal
   → Valores largos (1/4+): notas ligadas, efecto de pad

3. RANGE (rango de octavas):
   → 0: solo las notas presionadas (sin extensión)
   → +1: un octava adicional
   → +2: dos octavas
   → +3: tres octavas (rango amplio, dramático)

4. SWING:
   → 0ms: tiempo recto, mecánico
   → Valores medios: groove natural
   → Valores altos: shuffle pronunciado

5. SPLIT:
   → ALL: arpeggio en todo el teclado
   → RIGHT SIDE ONLY: arpeggio solo en zona derecha (requiere split activo)
   → LEFT SIDE ONLY: arpeggio solo en zona izquierda (bajo arpegiado + melodía libre)
```

### Técnicas de Arpeggio en Directo

#### Técnica 1: Latch + Manos Libres

```
1. Mantén presionado un acorde (ej. Am: A-C-E)
2. Activa [A LATCH]
3. Suelta las teclas → el arpeggio continúa solo
4. Con la mano derecha toca melodía encima
5. Para cambiar el acorde: presiona el nuevo acorde mientras el latch está activo
   → El arpeggio cambia instantáneamente al nuevo acorde

Para detener: presiona [A LATCH] de nuevo para desactivar el latch
```

#### Técnica 2: Control de Tempo con Tap

```
[TEMPO] × 2 → establece el BPM por tap
→ El arpeggiador se sincroniza al nuevo tempo
→ Útil para ajustar en tiempo real al DJ o a una pista
→ También configurable desde: GLOBAL/MIDI → MIDI CLOCK → EXTERNAL
   (para sincronizar con MIDI Clock de FL Studio)
```

#### Técnica 3: Cambio de Estilo en Caliente

```
Durante la actuación:
[EDIT] → ARPEGGIATOR → STYLE → girar DATA → cambiar estilo
→ El cambio es instantáneo mientras el arpeggio sigue sonando
→ Practica esta navegación hasta que sea instintiva
```

#### Técnica 4: Arpeggio con Pedal de Sustain

```
Configura el pedal de sustain como ARP LATCH:
[GLOBAL] → MIDI → CHANGE CONTROL → presiona el pedal
→ TYPE: SUSTAIN PEDAL → selecciona "ARP LATCH"

En el show:
→ Presiona el pedal con el pie para activar/desactivar el latch
→ Libera ambas manos para tocar melodías u operar controles
```

#### Técnica 5: Split + Arpeggio en Zona Izquierda

```
MOTOR 61 configuración:
[EDIT] → KEYBOARD SPLIT → ON → punto de división (ej. C4)
[EDIT] → ARPEGGIATOR → SPLIT → LEFT SIDE ONLY

Resultado en vivo:
← Zona izquierda (C2-B3): bajo arpegiado automáticamente
   Zona derecha (C4-C7) →: melodía libre sin arpeggio

Efecto: simultáneamente bajo arpegiado + melodía expresiva
```

---

## 5. Botones de Transporte para Control del Set

### Configuración en MC Mode (Recomendada para Directo)

En MC Mode, los botones de transporte controlan FL Studio directamente:

```
[<<] (Rewind)   → Retrocede en la línea de tiempo / salta a marcador anterior
[>>] (Fast Fwd) → Avanza en la línea de tiempo / salta al marcador siguiente
[STOP]          → Detiene la reproducción
[PLAY]          → Inicia la reproducción
[LOOP]          → Activa/desactiva el bucle
[REC]           → Arma la grabación
```

### Estrategia de Set en Vivo con Transport Buttons

#### Opción A: Set Basado en Patterns de FL Studio

```
Estructura en FL Studio (Song Mode):
  ├── Pattern 1: Intro
  ├── Pattern 2: Verse 1
  ├── Pattern 3: Chorus
  ├── Pattern 4: Bridge
  └── Pattern 5: Outro

Uso en directo:
→ [PLAY] inicia el set desde la posición actual
→ [>>] / [<<] navega entre secciones
→ [LOOP] para extender una sección improvisando
→ [STOP] pausa para entre canciones
```

#### Opción B: Reproducción de Stem Tracks

```
En FL Studio:
→ Carga stems pre-producidos en el Mixer
→ Cada fader del MOTOR 61 controla el volumen de un stem:
  Fader 1 → Batería
  Fader 2 → Bajo
  Fader 3 → Acordes/Harmónicos
  Fader 4 → Melodía
  Fader 5 → Efectos/Texturas
  Fader 6-8 → Reservas para improv

→ [PLAY] / [STOP] del MOTOR 61 controla todo el set
→ Los faders crean mezcla dinámica en tiempo real
```

#### Opción C: Configuración en Modo MIDI (Transport Mode)

Si prefieres no usar MC Mode para el transporte:

```
[GLOBAL] → MIDI → TRANSPORT MODE → selecciona:

MMC → FL Studio responde a MIDI Machine Control estándar
      (Stop, Play, Record por SysEx MMC)

MIDI Control → Cada botón envía un CC específico
               → Requiere mapear en FL Studio vía MIDI Learn

MIDI Note → Cada botón envía una nota específica
             → Mapeable a cualquier función de FL Studio
```

---

## 6. Cambio de Presets en Vivo

### Método 1: Cambio Rápido con DATA Encoder

```
Durante la actuación (modo silencioso y rápido):

1. Presiona [PRESET]
   → Display: nombre del preset actual

2. Presiona el encoder [DATA]
   → Modo de selección activado

3. Gira [DATA] una posición
   → Display: nombre del siguiente preset

4. Presiona [DATA] para cargar
   → El preset se aplica instantáneamente
   → Tiempo total: ~2-3 segundos
```

### Método 2: Presets Numerados y Secuenciales

Para un set de 10 canciones:

```
Organización sugerida:
  Preset 1: "INTRO"
  Preset 2: "VERSO1"
  Preset 3: "CORO"
  Preset 4: "PUENTE"
  Preset 5: "FINAL"
  Preset 6: "JAM1"   ← presets de improv extra
  Preset 7: "BASS"
  Preset 8: "TEXTURA"

Durante el show:
→ Gira DATA exactamente un "click" para avanzar un preset
→ Practica hasta conocer los clicks de memoria
→ Los presets están ordenados numéricamente en la selección DATA
```

### Método 3: Program Change desde Pads (Cambio Instantáneo)

Para cambio ultra-rápido de presets de plugins:

```
PAD BANK 25-32 configurado con P.CHNG:

[P CHNG] en el MOTOR 61 → Presiona un pad:
  Pad 1 → Program Change 0  (Kit de batería 1)
  Pad 2 → Program Change 1  (Kit de batería 2)
  Pad 3 → Program Change 16 (Bajo sintetizador)
  Pad 4 → Program Change 48 (Cuerdas)
  etc.

Ventaja: Un solo golpe de pad cambia el sonido del plugin instantáneamente,
         sin interrumpir la actuación.
```

### Qué Cambia y Qué No al Cambiar de Preset

```
✅ Al cambiar preset en el MOTOR 61:
  → Asignaciones CC de faders, encoders y pads
  → Canal MIDI de cada control
  → Configuración del arpeggiador
  → Notas asignadas a los pads
  → Colores de los pads
  → Modo de velocidad

❌ Lo que NO cambia (porque es del DAW, no del hardware):
  → Instrumentos cargados en FL Studio
  → Volúmenes en el Mixer de FL Studio
  → Efectos y plugins activos
  → La canción o proyecto en reproducción
```

---

## 7. Estrategias de Faders para el Directo

### Faders Motorizados: Aprovechamiento en Vivo

Los faders se mueven solos al cambiar de sección en FL Studio (cuando un canal cambia de nivel por automatización). Esto es una herramienta poderosa:

```
Truco de directo:
1. Programa automatizaciones de volumen en FL Studio (Song Mode)
2. Los faders físicos se moverán solos siguiendo la automatización
3. El público ve movimiento "mágico" de los faders
4. Puedes sobreescribir tocando un fader manualmente:
   → Toca el fader cap primero (touch-ON)
   → Luego muévelo a tu posición deseada
   → FL Studio registra tu override (automation write mode)
```

### Recomendaciones de Uso de Faders en Directo

Del manual oficial del MOTOR 61:

> *"You will have the best results with slow movements on no more than 4 faders at a time."*

```
Reglas para faders en directo:
1. Toca el cap del fader PRIMERO, luego muévelo
   → Evita que el motor "luche" contra tu movimiento
2. Mueve máximo 4 faders simultáneamente
3. Movimientos lentos y suaves > movimientos bruscos
4. Si un fader salta de posición: tócalo primero, deja que el DAW actualice,
   luego muévelo a donde quieres
```

### Asignación de Faders para Show

```
Sugerencia de asignación para set en vivo (MC Mode):
  Faders 1-8 → Canales del Mixer (stems, grupos)
  Fader 9 (Master) → Volumen total de salida
  
  Encoders (en MC Mode):
  → V-Pot Assignment cambia según el banco de encoders:
    Encoder Banks 1-8  → Track (parámetros de pista)
    Encoder Banks 9-16 → Send (envíos a efectos)
    Encoder Banks 17-24 → Pan (paneo)
    Encoder Banks 25-32 → Plug-In (parámetros del plugin activo)
```

---

## 8. Tips para Actuaciones Estables

### 🔴 Hardware

```
1. SIEMPRE usa el adaptador de corriente 12V
   → Sin él los motores están desactivados y hay menos funcionalidad
   → Lleva un adaptador de repuesto si el show es importante

2. Cable USB de calidad y corto
   → Los cables USB largos o de mala calidad pueden causar dropouts MIDI
   → Máximo 2 metros de USB sin hub
   → Si necesitas más largo: usa un hub USB con alimentación propia

3. Evita hubs USB sin alimentación
   → Pueden causar reinicios del MOTOR 61 si el consumo es alto

4. Protege el teclado del calor
   → Los motores generan calor; mantén ventilación alrededor del teclado
   → No cubras el teclado con tela durante el show

5. Calibra los motores si notan irregularidades
   → [GLOBAL] → FADERS → MOTOR CALIBRATE
   → Hazlo en el soundcheck, no durante el show
```

### 🟡 Software FL Studio

```
6. Cierra todos los programas no necesarios
   → Navegadores, reproductores, antivirus en tiempo real (temporalmente)
   → Solo FL Studio debe usar la CPU durante el show

7. Configura el buffer de audio según el venue
   → Estudio/ensayo: 128-256 samples (baja latencia)
   → Directo con PA: 512-1024 samples (más estable, latencia audible pero aceptable)
   → Si hay cortes de audio: duplica el buffer

8. Usa ASIO driver (Windows) o CoreAudio (macOS)
   → MME/DirectSound tienen latencia alta y son inestables para directo

9. Guarda un proyecto de emergencia
   → Ten una versión del proyecto con rutas de audio absolutas
   → Si falla algo, puedes cargar el backup en segundos

10. Pre-carga todo el proyecto antes de salir al escenario
    → Los samples deben estar ya en RAM
    → Haz play/stop una vez para pre-cachear los plugins
```

### 🟢 Performance y Técnica

```
11. Practica los cambios de preset sin mirar el display
    → Debes saber cuántos giros de DATA necesitas para llegar a cada preset

12. Configura el arpeggiador antes de subir al escenario
    → No cambies la configuración de EDIT en medio del show si puedes evitarlo

13. Usa el pedal de sustain para latch del arpeggiador
    → Libera las manos para otros controles

14. Prepara dos presets "de emergencia":
    → "RESET": configuración limpia y simple por si algo falla
    → "SOLO": para si necesitas tocar solo piano sin complicaciones

15. Haz un soundcheck completo con el set real
    → Prueba cada cambio de preset
    → Verifica que los pads suenan en los monitores de escenario
    → Confirma que los faders controlan FL Studio correctamente
```

---

## 9. Checklist Pre-Show

### 30 Minutos Antes

```
HARDWARE:
☐ Adaptador 12V conectado y funcionando (LED sólido en MOTOR 61)
☐ USB conectado al laptop
☐ MC Mode activo (display muestra indicador MC)
☐ Pedal de sustain conectado y configurado (ej. ARP LATCH)
☐ Pedal de expresión conectado (si se usa)
☐ Audio de FL Studio → interfaz → PA verificado

SOFTWARE (FL Studio):
☐ Proyecto del set cargado y guardado
☐ MIDIIN2 configurado como Mackie Control Universal
☐ MOTOR61 (Puerto 1) habilitado para notas
☐ Todos los samples y plugins cargados (sin "missing files")
☐ Buffer de audio ajustado para el venue
☐ Modo de alto rendimiento activado en el sistema operativo

MOTOR 61:
☐ Preset 1 cargado (inicio del set)
☐ Todos los presets necesarios guardados y nombrados
☐ Colores de pads configurados y verificados
☐ Faders en posición inicial (hacer un play/stop en FL Studio para sincronizar)
☐ Arpeggiador configurado (tempo, estilo, rango)
```

### 10 Minutos Antes

```
☐ Prueba cada pad del banco 1-8: todos suenan correctamente
☐ Prueba los botones de transporte: PLAY y STOP funcionan
☐ Prueba los faders: se mueven y controlan el mixer de FL Studio
☐ Prueba el arpeggiador con [ARPEG] + algunas teclas
☐ Verifica el volumen de cada stem en los monitores
☐ Haz un cambio de preset completo (Preset 1 → Preset 2 → Preset 1)
☐ Confirma que el laptop no entrará en suspensión
☐ Cierra el navegador y cualquier programa innecesario
```

---

## 10. Recuperación de Errores en Vivo

### Escenario 1: Faders Dejan de Responder

```
Causa probable: Desincronización MC
Solución rápida (15 segundos):
  1. En FL Studio: cierra y reabre el Mixer [F9]
  2. Si no funciona: Options → MIDI Settings → desactiva MIDIOUT2 → reactiva
  3. Último recurso: apaga y enciende el MOTOR 61 con USB conectado
```

### Escenario 2: Notas del Teclado No Suenan

```
Causa probable: Canal MIDI desalineado o instrumento sin foco
Solución rápida (5 segundos):
  1. Clic en el instrumento activo en el Channel Rack de FL Studio
  2. Si no funciona: verifica que MOTOR61 (Puerto 1) está activo en MIDI Settings
```

### Escenario 3: Audio con Cortes (Glitches)

```
Causa probable: Buffer muy pequeño o CPU saturada
Solución rápida:
  1. Options → Audio settings → aumenta Buffer Length (duplica el valor)
  2. Si persiste: cierra ventanas innecesarias de FL Studio
  3. Desactiva visualizaciones que consuman CPU (peak meters, análisis espectral)
```

### Escenario 4: Preset Corrupto o No Carga Bien

```
Causa probable: Preset guardado con configuración incorrecta
Solución rápida:
  1. Presiona [PRESET] → DATA → navega al DEFAULT (Preset 0)
  2. El DEFAULT siempre está disponible como punto de retorno
  3. Continúa el show con la configuración base
```

### Escenario 5: MOTOR 61 No Responde al Reiniciarlo en Vivo

```
Procedimiento de reinicio de emergencia:
  1. Apaga MOTOR 61 con el interruptor
  2. Espera 5 segundos
  3. Enciende MOTOR 61
  4. Espera a que aparezca el logo/display → MC Mode se activa automáticamente
     (si fue guardado previamente)
  5. FL Studio debería reconectar automáticamente
  6. Si no: Options → MIDI Settings → desactiva/activa los puertos del MOTOR 61
```

---

> **Ver también:**
> - [PRESETS_GUIA.md](PRESETS_GUIA.md) — Gestión detallada de presets
> - [ASIGNACION_NOTAS_CC.md](ASIGNACION_NOTAS_CC.md) — Asignaciones de CC y Notas
> - [PROBLEMAS_COMUNES.md](PROBLEMAS_COMUNES.md) — Árbol de diagnóstico completo
> - [MC_MODE_TABLA.md](MC_MODE_TABLA.md) — Tabla de funciones Mackie Control
