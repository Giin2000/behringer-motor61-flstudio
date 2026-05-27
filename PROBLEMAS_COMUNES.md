# 🔧 Problemas Comunes y Soluciones — Behringer MOTOR 61 + FL Studio 2025

> **← Volver al [README](README.md)**

---

## Índice de Problemas

| # | Síntoma | Saltar a |
|---|---|---|
| 1 | Los faders no se mueven | [→](#1-los-faders-no-se-mueven-motores-inactivos) |
| 2 | FL Studio no reconoce el MOTOR 61 | [→](#2-fl-studio-no-reconoce-el-motor-61) |
| 3 | El teclado no produce sonido | [→](#3-el-teclado-no-produce-sonido) |
| 4 | Los faders se mueven pero a posición incorrecta | [→](#4-los-faders-se-mueven-pero-a-posición-incorrecta) |
| 5 | Botones de transporte no responden | [→](#5-botones-de-transporte-no-responden) |
| 6 | El display del MOTOR 61 no muestra nombres de canales | [→](#6-el-display-no-muestra-nombres-de-canales) |
| 7 | MIDIIN2/MIDIOUT2 no aparecen en FL Studio | [→](#7-midiin2midiout2-no-aparecen-en-fl-studio) |
| 8 | Los motores hacen ruido pero no se posicionan bien | [→](#8-los-motores-hacen-ruido-pero-no-se-posicionan-correctamente) |
| 9 | Doble entrada MIDI (notas duplicadas) | [→](#9-doble-entrada-midi-notas-duplicadas) |
| 10 | MC Mode se desactiva solo al apagar | [→](#10-mc-mode-se-desactiva-al-apagar) |

---

## 1. Los Faders no se Mueven (Motores Inactivos)

### Síntoma
Los faders físicos no responden cuando se mueven controles en FL Studio. No hay resistencia al moverlos manualmente.

### Causa más probable: ⚡ Falta el adaptador 12V

```
DIAGNÓSTICO RÁPIDO:
¿Está conectado el adaptador de corriente 12V DC?  
├── NO → Conectarlo es la solución completa
└── SÍ → Continúa con los siguientes pasos
```

### Árbol de Diagnóstico Completo

```
Faders no se mueven
│
├── ¿Adaptador 12V conectado?
│   ├── NO ──→ [SOLUCIÓN] Conecta el adaptador 12V original
│   │           Los motores requieren alimentación externa.
│   │           El USB solo alimenta la electrónica, no los motores.
│   │
│   └── SÍ ──→ ¿MC Mode activo?
│               ├── NO ──→ [SOLUCIÓN] Activar MC Mode
│               │           Ver: MC_MODE_TABLA.md
│               │
│               └── SÍ ──→ ¿MIDIOUT2 configurado en FL Studio?
│                           ├── NO ──→ [SOLUCIÓN] Configurar salida MIDIOUT2
│                           │           con Mackie Control Universal
│                           │
│                           └── SÍ ──→ ¿Los puertos coinciden? (puerto 2 → puerto 2)
│                                       ├── NO ──→ Corregir numeración de puertos
│                                       └── SÍ ──→ Reinstalar drivers / reiniciar
```

### Solución Paso a Paso

1. **Verifica la alimentación:**  
   - LED de encendido debe estar sólido (no parpadeando)
   - El adaptador debe marcar `12V DC` en la etiqueta
   
2. **Verifica MC Mode:** Ver [MC_MODE_TABLA.md](MC_MODE_TABLA.md)

3. **Verifica la salida MIDI:**
   ```
   FL Studio → Options → MIDI Settings
   → MIDIOUT2 (MOTOR61) debe estar habilitado
   → Controller type: Mackie Control Universal
   → Puerto: 2
   ```

4. **Prueba de motor manual:**  
   Apaga y enciende el MOTOR 61. Al encenderse, los faders deben hacer un movimiento de "home" (van a cero y vuelven a la posición guardada).

---

## 2. FL Studio no Reconoce el MOTOR 61

### Síntoma
El nombre `MOTOR61` o `MIDIIN2` no aparece en la lista de dispositivos MIDI de FL Studio.

### Soluciones

#### Solución A: Reconexión USB

```
1. Cierra FL Studio completamente
2. Desconecta el USB del MOTOR 61
3. Espera 10 segundos
4. Reconecta el USB
5. Abre FL Studio
6. Ve a Options → MIDI Settings
7. Pulsa "Refresh" si existe esa opción
```

#### Solución B: Problema de Driver (Windows)

```
1. Administrador de dispositivos → Controladores de sonido, vídeo y juegos
2. Busca: "Behringer" o "MOTOR 61" o "USB Audio CODEC"
3. ¿Aparece con ícono de error (⚠️ o ❌)?
   → Clic derecho → Desinstalar dispositivo
   → Desconecta USB
   → Reinstala driver desde behringer.com
   → Reconecta USB
4. ¿No aparece en absoluto?
   → Prueba otro puerto USB (preferiblemente USB 2.0)
   → Evita hubs USB; conecta directamente al ordenador
```

#### Solución C: Conflicto con otros dispositivos MIDI

```
1. Desconecta todos los demás dispositivos MIDI/USB temporalmente
2. Conecta solo el MOTOR 61
3. Verifica si ahora aparece en FL Studio
4. Si funciona, reconecta los demás dispositivos uno a uno para identificar el conflicto
```

---

## 3. El Teclado no Produce Sonido

### Síntoma
Se presionan teclas pero no se escucha ningún sonido. FL Studio no registra notas.

### Diagnóstico

| Verificación | Cómo comprobar |
|---|---|
| ¿Puerto 1 habilitado? | `MIDI Settings` → `MOTOR61` (puerto 1) → debe estar ✅ activo |
| ¿Canal MIDI correcto? | El instrumento virtual debe recibir en `Canal 1` o `Todos` |
| ¿Instrumento abierto? | Debe haber un instrumento activo en el canal seleccionado del Step Sequencer |
| ¿Volumen del canal? | Verifica que el canal no esté en mute o silenciado |

### Solución

```
1. MIDI Settings → Busca "MOTOR61" o "MIDIIN (MOTOR61)"
   → Asegúrate de que esté habilitado (✅)
   → Port: 1 (o el valor por defecto)

2. En FL Studio, crea un canal de instrumento nuevo:
   → Channel Rack → Clic derecho → "Add one" → Elige un instrumento (ej. FLEX)

3. El canal debe estar seleccionado (resaltado en verde)

4. Toca una tecla → debe verse actividad en el piano roll y sonar el instrumento

5. Si aún no funciona: Options → MIDI Settings → "Send master sync" debe estar activo
```

---

## 4. Los Faders se Mueven pero a Posición Incorrecta

### Síntoma
Los motores están activos, los faders se mueven, pero los valores no corresponden a los niveles del mixer de FL Studio.

### Causas y Soluciones

**Causa A: Desfase de canal (bank offset)**
```
Los faders del MOTOR 61 pueden estar en "banco 2" mientras FL Studio muestra "banco 1"
→ Presiona BANK LEFT (<<) en el MOTOR 61 para volver al banco 1
→ Los faders deben realinearse automáticamente
```

**Causa B: Puerto incorrecto**
```
Si MIDIOUT2 está configurado en puerto 1 en lugar de puerto 2:
→ MIDI Settings → MIDIOUT2 → verificar que el número de puerto sea 2
→ Debe coincidir con la entrada MIDIIN2 también en puerto 2
```

**Causa C: Necesita resincronización**
```
1. Cierra el proyecto en FL Studio (sin cerrar FL Studio)
2. Apaga y enciende el MOTOR 61
3. Vuelve a abrir el proyecto
4. Los faders deben ir a las posiciones correctas al cargarse
```

---

## 5. Botones de Transporte no Responden

### Síntoma
PLAY, STOP, REC del MOTOR 61 no controlan FL Studio.

### Verificación Rápida

```
¿MC Mode activo? → Ver MC_MODE_TABLA.md
¿MIDIIN2 configurado con Mackie Control Universal? → Ver CONFIGURACION_FL_STUDIO.md
```

### Solución

```
1. MIDI Settings → MIDIIN2 → Controller type: "Mackie Control Universal"
   (Si está en "Generic Controller" o "Ninguno", cambiarlo)

2. Asegúrate de que el puerto de entrada (MIDIIN2) y salida (MIDIOUT2) coincidan

3. En FL Studio → Mixer → verifica que el mixer esté visible
   (algunos comandos MC solo funcionan si el Mixer está abierto)

4. Reinicia FL Studio con el MOTOR 61 ya conectado y en MC Mode
```

---

## 6. El Display no Muestra Nombres de Canales

### Síntoma
La pantalla LCD del MOTOR 61 muestra valores vacíos, raros o no actualiza los nombres de los canales del mixer.

### Causa
FL Studio no está enviando datos de retorno al MOTOR 61 (falta la salida MIDI configurada).

### Solución

```
1. MIDI Settings → Pestaña OUTPUT (salida)
2. Busca MIDIOUT2 (MOTOR61)
3. Habilitarlo con ✅
4. Asignar Controller type: Mackie Control Universal
5. Puerto: 2
6. Cerrar y reabrir FL Studio
```

> **Nota:** El display del MOTOR 61 solo mostrará información cuando FL Studio  
> tenga configurada correctamente la **salida** MIDIOUT2. Sin ella, es comunicación unidireccional.

---

## 7. MIDIIN2/MIDIOUT2 no Aparecen en FL Studio

### Síntoma
Solo aparece `MOTOR61` (un único puerto) pero no `MIDIIN2` ni `MIDIOUT2`.

### Causas

**Causa A: MC Mode desactivado en el hardware**
```
El MOTOR 61 solo expone el Puerto 2 (MIDIIN2/MIDIOUT2) cuando MC Mode está ACTIVO.
→ Activa MC Mode en el teclado (ver MC_MODE_TABLA.md)
→ Desconecta y reconecta el USB
→ Abre FL Studio → MIDI Settings
→ Ahora MIDIIN2 y MIDIOUT2 deben aparecer
```

**Causa B: Driver desactualizado**
```
Drivers más antiguos solo exponen 1 puerto.
→ Actualiza al driver más reciente desde behringer.com
```

**Causa C: Puerto USB con limitaciones**
```
Algunos hubs USB o puertos USB 3.0 tienen problemas con dispositivos MIDI de doble puerto.
→ Prueba conectar directamente en un puerto USB 2.0 de la placa base
```

---

## 8. Los Motores Hacen Ruido pero no se Posicionan Correctamente

### Síntoma
Se escucha el motor intentando moverse pero el fader vibra, oscila o no llega a la posición correcta.

### Causas y Soluciones

**Causa A: Calibración necesaria**
```
1. Apaga el MOTOR 61
2. Desconecta el USB y el adaptador 12V
3. Espera 30 segundos
4. Reconecta todo y enciende
5. Los motores realizarán una recalibración automática al encenderse
```

**Causa B: Interferencia de señal**
```
El cable USB puede estar captando interferencias si está enrollado cerca del adaptador de corriente.
→ Separa físicamente el cable USB del cable de alimentación 12V
→ Usa un cable USB blindado si el problema persiste
```

**Causa C: Fader mecánicamente atascado**
```
1. Con el teclado apagado, mueve el fader manualmente por todo su recorrido varias veces
2. Verifica que no haya suciedad u objeto obstruyendo el rail del fader
3. Si el fader no se mueve suavemente a mano, puede necesitar servicio técnico
```

---

## 9. Doble Entrada MIDI (Notas Duplicadas)

### Síntoma
Cada nota suena dos veces o aparece duplicada en el piano roll al grabar.

### Causa
Tanto el Puerto 1 (`MOTOR61`) como el Puerto 2 (`MIDIIN2`) están habilitados como entrada de notas simultáneamente.

### Solución

```
MIDI Settings → INPUT
→ MIDIIN2 (MOTOR61): Controller type = "Mackie Control Universal"
  Este puerto NO debe estar activo para entrada de notas generales.

→ MOTOR61 (Puerto 1): habilitado para notas ✅
  Este es el único puerto que debe enviar notas a los instrumentos.

Regla: Solo un puerto debe alimentar las notas. El puerto MC (2) tiene su propio controlador asignado.
```

---

## 10. MC Mode se Desactiva al Apagar

### Síntoma
Cada vez que se apaga y enciende el MOTOR 61, el MC Mode ha vuelto al modo estándar.

### Causa
El MC Mode no se guardó correctamente en la memoria del dispositivo.

### Solución

```
Procedimiento de guardado permanente de MC Mode:
1. Activa MC Mode (ver MC_MODE_TABLA.md)
2. Mantén presionado [SETUP] durante 3 segundos mientras MC está activo
3. El display debe mostrar "SAVED" o una confirmación similar
4. Apaga y enciende → MC Mode debe persistir

Alternativa: algunos modelos requieren:
[SETUP] + [STORE/SAVE] simultáneamente para guardar en memoria no volátil
```

---

## Tabla Resumen de Diagnóstico Rápido

| Problema | Primera acción | Segunda acción |
|---|---|---|
| Motores no se mueven | Verificar adaptador 12V | Verificar MC Mode |
| MOTOR61 no aparece | Reconectar USB | Reinstalar driver |
| Sin sonido | Habilitar Puerto 1 en MIDI Settings | Verificar instrumento activo |
| Faders en posición incorrecta | Presionar BANK LEFT | Verificar puertos (ambos en 2) |
| Transporte no responde | Verificar MC Mode activo | Controller type = Mackie Control |
| MIDIIN2 no aparece | Activar MC Mode en hardware | Reconectar USB |
| Notas duplicadas | Verificar solo Puerto 1 para notas | MIDIIN2 solo para MC |

---

> ¿El problema no está en esta lista? Abre un [Issue en GitHub](../../issues) describiendo:  
> - Versión de FL Studio  
> - Versión de Windows/macOS  
> - Versión del firmware del MOTOR 61 (visible en el display al encender)  
> - Pasos exactos para reproducir el problema
