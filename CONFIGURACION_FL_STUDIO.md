# ⚙️ Configuración Detallada — Behringer MOTOR 61 en FL Studio 2025

> **← Volver al [README](README.md)**

---

## Índice

1. [Preparación del Hardware](#1-preparación-del-hardware)
2. [Activar MC Mode en el MOTOR 61](#2-activar-mc-mode-en-el-motor-61)
3. [Configuración de MIDI en FL Studio](#3-configuración-de-midi-en-fl-studio)
4. [Asignación de Puertos — Guía Visual](#4-asignación-de-puertos--guía-visual)
5. [Vincular el Surface Controller](#5-vincular-el-surface-controller)
6. [Verificación y Prueba Final](#6-verificación-y-prueba-final)
7. [Configuración de Canales de Mixer](#7-configuración-de-canales-de-mixer)
8. [Personalización Adicional](#8-personalización-adicional)

---

## 1. Preparación del Hardware

### Lista de verificación física

```
☐  Adaptador 12V DC conectado al MOTOR 61
☐  Cable USB tipo B conectado al ordenador
☐  MOTOR 61 encendido (botón POWER)
☐  Drivers instalados (Windows: ver sección Drivers)
```

### ⚠️ Sobre el Adaptador de Corriente 12V

**Este es el error más común de todos los usuarios.**

| Estado del adaptador | Resultado |
|---|---|
| ✅ Conectado y encendido | Faders motorizados ACTIVOS, motores responden |
| ❌ Desconectado | Faders NO se mueven, motores completamente INACTIVOS |
| ❌ Voltaje incorrecto | Riesgo de daño al hardware — usa solo el adaptador original |

> El teclado puede encenderse y enviar MIDI **sin** el adaptador 12V (alimentado por USB),  
> pero los motores de los faders **requieren la alimentación externa** para operar.

### Instalación de Drivers (Windows)

1. Descarga el driver desde: [behringer.com/downloads](https://www.behringer.com) → busca "MOTOR 61"
2. Ejecuta el instalador **con el MOTOR 61 desconectado**
3. Reinicia el sistema cuando se solicite
4. Conecta el MOTOR 61 por USB
5. Verifica en `Administrador de Dispositivos` → `Controladores de sonido, vídeo y juegos`

> **macOS:** No requiere driver adicional. El MOTOR 61 es reconocido automáticamente como dispositivo CoreMIDI/CoreAudio.

---

## 2. Activar MC Mode en el MOTOR 61

**El MC Mode debe estar activo SIEMPRE para que FL Studio reconozca la superficie de control.**  
Si el modo no está activo, los faders, botones y encoders no enviarán mensajes Mackie Control.

### Procedimiento de Activación

```
1. Con el teclado encendido, mantén presionado: [SETUP]
2. Mientras mantienes [SETUP], presiona el botón asignado a "MC MODE"
   (generalmente marcado o indicado en la pantalla)
3. La pantalla debe mostrar: "MC" o "MACKIE" o un indicador LED
4. Suelta los botones
5. El modo queda guardado en memoria no volátil
```

> Para la combinación exacta de botones según versión de firmware,  
> consulta la tabla completa en [MC_MODE_TABLA.md](MC_MODE_TABLA.md).

### Verificación del MC Mode

- El display del MOTOR 61 debería mostrar un indicador de modo activo
- Al mover un fader manualmente, debe resistirse levemente (motor activo)
- Los botones de transporte (PLAY, STOP, REC) deben iluminarse con señal MC

---

## 3. Configuración de MIDI en FL Studio

### Abrir MIDI Settings

```
FL Studio → Options (menú superior) → MIDI Settings
           ─── o ───
           Atajo de teclado: ninguno por defecto
           ─── o ───
           F10 → pestaña MIDI
```

### Vista general de la ventana MIDI Settings

```
┌─────────────────────────────────────────────────────────────┐
│  MIDI SETTINGS                                               │
├──────────────────────────┬──────────────────────────────────┤
│  INPUT                   │  OUTPUT                          │
│  ──────────────────────  │  ──────────────────────────────  │
│  □ MOTOR61               │  □ MOTOR61                       │
│  ■ MIDIIN2 (MOTOR61)     │  ■ MIDIOUT2 (MOTOR61)            │
│                          │                                  │
│  Controller type:        │                                  │
│  [Mackie Control     ▼]  │                                  │
│                          │                                  │
│  Port: [2]               │  Port: [2]                       │
└──────────────────────────┴──────────────────────────────────┘
```

---

## 4. Asignación de Puertos — Guía Visual

### Puerto 1 — Teclado / Instrumento

| Campo | Valor |
|---|---|
| Dispositivo | `MOTOR61` o `MIDIIN (MOTOR61)` |
| Habilitado | ✅ Sí |
| Tipo de controlador | `(Generic controller)` o dejarlo en blanco |
| Puerto | `1` o el asignado automáticamente |
| Uso | Tocar notas, velocity, pitch bend, modulación |

### Puerto 2 — Mackie Control (Superficie de Control)

| Campo | Valor |
|---|---|
| Dispositivo de entrada | `MIDIIN2 (MOTOR61)` |
| Dispositivo de salida | `MIDIOUT2 (MOTOR61)` |
| Habilitado | ✅ Sí (ambos) |
| Tipo de controlador | `Mackie Control Universal` |
| Puerto | `2` |
| Uso | Faders, botones de transporte, encoders, LEDs |

> **¿Por qué el Puerto 2 para MC?**  
> Behringer implementa una arquitectura de doble puerto: el Puerto 1 envía datos de teclado  
> estándar (MIDI general), mientras que el Puerto 2 está dedicado exclusivamente al  
> protocolo Mackie Control bidireccional, que requiere comunicación de ida y vuelta  
> para mover los faders y actualizar los indicadores LED.

---

## 5. Vincular el Surface Controller

### Añadir el controlador en FL Studio

1. En `MIDI Settings`, selecciona `MIDIIN2` en la lista de entradas
2. Cambia el **Controller type** a `Mackie Control Universal`
3. En el campo **Output**, selecciona `MIDIOUT2`
4. Haz clic en **Enable** (habilitarlo)
5. Asegúrate de que el número de puerto sea `2` en ambos campos
6. Cierra la ventana → FL Studio debería inicializar la comunicación automáticamente

### Confirmación Visual

Cuando la configuración es correcta:
- Los faders del MOTOR 61 se mueven solos al abrir FL Studio (posición inicial)
- El display del teclado muestra el nombre del canal del mixer activo
- Los botones de transporte reflejan el estado de Play/Stop de FL Studio

---

## 6. Verificación y Prueba Final

### Test de Faders

```
1. Abre FL Studio con un proyecto que tenga canales de mixer
2. Los faders físicos deben ajustarse automáticamente a los niveles del proyecto
3. Mueve un fader manualmente → el nivel del canal en FL Studio debe cambiar
4. Mueve el fader de volumen master en FL Studio → el fader físico debe moverse
```

### Test de Transporte

```
1. Presiona PLAY en el MOTOR 61 → FL Studio debe iniciar reproducción
2. Presiona STOP → FL Studio debe detenerse
3. Presiona REC → FL Studio debe entrar en modo grabación
```

### Test de Teclado (Puerto 1)

```
1. Abre un instrumento virtual en FL Studio (piano, sintetizador, etc.)
2. Toca las teclas del MOTOR 61
3. Deben sonar notas en el instrumento seleccionado
4. La velocidad (velocity) debe reflejarse según la fuerza de pulsación
```

---

## 7. Configuración de Canales de Mixer

### Navegar por Canales con el MOTOR 61

El MOTOR 61 generalmente controla **8 canales del mixer simultáneamente** en modo MC:

```
┌────┬────┬────┬────┬────┬────┬────┬────┐
│ CH1│ CH2│ CH3│ CH4│ CH5│ CH6│ CH7│ CH8│  ← Página actual
└────┴────┴────┴────┴────┴────┴────┴────┘
         ← BANK L │ BANK R →              ← Cambiar página de 8 en 8
         ← CH L   │ CH R   →              ← Desplazar de 1 en 1
```

### Botones de Navegación MC

| Botón en MOTOR 61 | Función en FL Studio |
|---|---|
| `BANK L` / `<<` | Retrocede 8 canales en el mixer |
| `BANK R` / `>>` | Avanza 8 canales en el mixer |
| `CH L` / `<` | Retrocede 1 canal |
| `CH R` / `>` | Avanza 1 canal |

---

## 8. Personalización Adicional

### Scripts MIDI Personalizados

FL Studio permite usar scripts Python personalizados para el MOTOR 61:

1. Navega a: `%USERPROFILE%\Documents\Image-Line\FL Studio\Settings\Hardware`
2. Copia la carpeta de scripts para Mackie Control
3. Edita el archivo `.py` para reasignar botones según tus necesidades

### Guardar Configuración como Preset

```
MIDI Settings → Controller type → [Mackie Control Universal]
→ Botón de guardar (ícono de disquete o "Save preset")
→ Nombra el preset: "MOTOR61_MC_Config"
```

Esto preserva toda la configuración de puertos y controlador para futuros proyectos.

---

> **Siguiente paso:** Consulta [PROBLEMAS_COMUNES.md](PROBLEMAS_COMUNES.md) si algo no funciona como se esperaba.  
> **Referencia rápida:** Ver [MC_MODE_TABLA.md](MC_MODE_TABLA.md) para la tabla completa de funciones.
