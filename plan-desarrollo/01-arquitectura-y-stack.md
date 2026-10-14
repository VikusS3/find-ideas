# Arquitectura Técnica y Stack Tecnológico

> **Documento:** 01 - Arquitectura y Stack  
> **Fecha:** Octubre 2026  
> **Propósito:** Definir el diseño de software, el Project JSON Schema, el flujo de datos y la separación entre Editor y Runtime.

---

## 1. Stack Tecnológico Seleccionado

| Componente | Elección | Justificación Técnica |
| :--- | :--- | :--- |
| **Build Tool & Bundler** | **Vite + TypeScript** | Arranque instantáneo (HMR <50ms), compilación optimizada en ES Modules nativos. |
| **Framework UI del Editor** | **React 19 + Tailwind CSS** | Amplio ecosistema para componentes de tooling (docking panels, sliders, context menus, color pickers) y excelente soporte tipado. |
| **Gestor de Estado del Editor** | **Zustand + Immer** | Estado reactivo fuera del árbol de React con overhead mínimo (<3KB), perfecto para el patrón Command/Undo-Redo sin re-renderizar todo el canvas. |
| **Motor 2D (MVP)** | **Phaser 3 / 4** | ~1 MB gzip; incluye ciclo de juego (game loop), física arcade integrada, tilemaps ortogonales e isométricos, manejo de sprites/atlas y audio HTML5/WebAudio. |
| **Motor 3D (Fase 2)** | **Three.js + Rapier** | Render WebGL/WebGPU ligero (~600KB) + física de cuerpos rígidos compilada en WebAssembly (Rapier), sin sobrecarga de motores cerrados. |
| **Editor de Código** | **Monaco Editor** | El motor de VS Code embebido como librería web (MIT). Permite autocompletado y validación TypeScript sin incurrir en los 200 MB de Electron. |
| **Almacenamiento Local** | **OPFS (Origin Private File System) + IndexedDB** | Almacenamiento local-first con lectura/escritura de alta velocidad para texturas y audio sin límites restrictivos de LocalStorage. |
| **Capa Desktop** | **Tauri 2.0 (Rust)** | Binario final <15 MB utilizando el WebView nativo del sistema operativo (WebView2 en Windows, WebKit en macOS/Linux). |
| **Capa Móvil** | **Capacitor 6** | Wrapper ligero que expone el runtime del juego como app híbrida en Android e iOS sin dependencias pesadas. |

---

## 2. Diagrama de Arquitectura de Alto Nivel

```
+---------------------------------------------------------------------------------------+
|                                    CAPA DE PRESENTACIÓN                               |
|                                                                                       |
|   +-------------------+  +-------------------+  +------------------+  +-----------+   |
|   | Hierarchy (Árbol) |  | Viewport 2D/3D    |  | Property         |  | Asset     |   |
|   | & Scene Manager   |  | (Gizmos/Overlays) |  | Inspector        |  | Browser   |   |
|   +---------+---------+  +---------+---------+  +--------+---------+  +-----+-----+   |
|             |                      |                     |                  |         |
|             +----------------------+---------------------+------------------+         |
|                                    |                                                  |
|                                    v                                                  |
|                        [ Zustand Central Store ]                                      |
|               (Historial Undo/Redo, Selección, Metadatos)                             |
+------------------------------------+--------------------------------------------------+
                                     |
               (Sincronización bidireccional de Schema)
                                     |
                                     v
+------------------------------------+--------------------------------------------------+
|                             CAPA DE MOTOR Y RUNTIME                                   |
|                                                                                       |
|   +-------------------------------------------------------------------------------+   |
|   | Sandbox IFrame Aislado (Playtest & Preview)                                   |   |
|   |                                                                               |   |
|   |  +-------------------------+     +-----------------------------------------+  |   |
|   |  | Runtime Engine Bridge   | <-> | Motor Phaser 2D / Three.js 3D           |  |   |
|   |  | (Event Loop, Hot-Reload)|     | (Física, Render, Input, Audio)          |  |   |
|   |  +-------------------------+     +-----------------------------------------+  |   |
|   +-------------------------------------------------------------------------------+   |
+------------------------------------+--------------------------------------------------+
                                     |
                                     v
+------------------------------------+--------------------------------------------------+
|                            SERVICIOS Y PERSISTENCIA                                   |
|                                                                                       |
|   +------------------------+  +-----------------------+  +------------------------+   |
|   | Storage Local (OPFS)   |  | AI Hub (Workers AI    |  | Export Pipeline        |   |
|   | Proyectos, Assets CC0  |  | + BYOK Client)        |  | Web ZIP / Tauri Build  |   |
|   +------------------------+  +-----------------------+  +------------------------+   |
+---------------------------------------------------------------------------------------+
```

---

## 3. Desacoplamiento Fundamental: Editor vs. Runtime

Uno de los principales errores en los clones de Unity es acoplar la interfaz del editor a la instancia viva del motor. Para garantizar estabilidad, rendimiento y seguridad:

1. **Aislamiento en IFrame o WebWorker:**
   - La ventana de edición visual y el modo de "Playtest" residen en un contexto independiente.
   - Si un script de usuario produce un bucle infinito o un `TypeError` fatal, el editor principal no se congela ni pierde los cambios no guardados.
2. **Puente de Comunicación (`MessagePort` / `postMessage` tipado):**
   - El editor envía mutaciones del esquema de juego (`UPDATE_ENTITY_TRANSFORM`, `SPAWN_PREFAB`, `EXECUTE_EVENT`).
   - El runtime notifica telemetría básica (FPS, consumo de memoria, logs de consola interceptados).
3. **Modo Edición vs. Modo Ejecución:**
   - En **Modo Edición**, el canvas dibuja las guías visuales (grid, gizmos de traslación, bounding boxes de colisionadores) y los sistemas de física están pausados.
   - En **Modo Playtest**, se clona el estado en memoria del proyecto, se inicializa el bucle de física de Phaser y se activa la captura de inputs de teclado/ratón/gamepad.

---

## 4. Especificación del Project JSON Schema (`v1.0.0`)

El formato del proyecto es un archivo JSON estándar, autodocumentado y validable mediante **Zod / JSON Schema**. Este archivo representa la verdad canónica del proyecto.

```json
{
  "$schema": "https://raw.githubusercontent.com/find-ideas/light-engine/main/schemas/project-v1.json",
  "name": "Super Plat Plat",
  "version": "1.0.0",
  "engine": "phaser-2d",
  "canvas": {
    "width": 800,
    "height": 600,
    "pixelArt": true,
    "backgroundColor": "#1a1a24"
  },
  "physics": {
    "system": "arcade",
    "gravity": { "x": 0, "y": 600 },
    "debug": false
  },
  "assets": [
    {
      "id": "asset-hero-sheet",
      "type": "spritesheet",
      "name": "hero.png",
      "path": "assets/hero.png",
      "license": {
        "source": "Kenney.nl",
        "type": "CC0",
        "author": "Kenney"
      },
      "metadata": {
        "frameWidth": 32,
        "frameHeight": 32
      }
    }
  ],
  "scenes": [
    {
      "id": "scene-level-1",
      "name": "Nivel 1 - Bosque",
      "isInitial": true,
      "entities": [
        {
          "id": "ent-player-01",
          "name": "Player",
          "tag": "Player",
          "transform": {
            "position": { "x": 100, "y": 300 },
            "rotation": 0,
            "scale": { "x": 1, "y": 1 }
          },
          "components": [
            {
              "type": "SpriteRenderer",
              "properties": {
                "assetId": "asset-hero-sheet",
                "currentFrame": 0
              }
            },
            {
              "type": "ArcadeBody",
              "properties": {
                "immovable": false,
                "collideWorldBounds": true,
                "drag": { "x": 200, "y": 0 }
              }
            },
            {
              "type": "PlatformerController",
              "properties": {
                "moveSpeed": 220,
                "jumpForce": -420
              }
            }
          ]
        }
      ],
      "events": [
        {
          "id": "evt-on-coin-collected",
          "trigger": "collision",
          "targetA": "Player",
          "targetB": "Coin",
          "actions": [
            { "type": "DestroyEntity", "params": { "target": "other" } },
            { "type": "AddScore", "params": { "amount": 10 } },
            { "type": "PlaySound", "params": { "assetId": "snd-coin-pickup" } }
          ]
        }
      ]
    }
  ]
}
```

---

## 5. Patrón de Gestión de Estado y Undo/Redo

Para lograr una experiencia de edición fluida, se utiliza el patrón **Command Pattern** acoplado al store de Zustand:

1. **Estructura de Comandos:**
   ```typescript
   export interface EditorCommand {
     name: string;
     execute: (state: ProjectState) => void;
     undo: (state: ProjectState) => void;
   }
   ```
2. **Pila de Deshacer (Undo Stack):**
   - Límite de 50 pasos de historial para no saturar memoria.
   - Las mutaciones continuas (ej. arrastrar una entidad con el ratón) agrupan sus deltas en una sola transacción (`transaction.start()` al mousedown, `transaction.commit()` al mouseup).
3. **Persistencia Local Automática:**
   - Un worker secundario guarda una copia del snapshot del proyecto en **OPFS** cada 3 segundos tras la última modificación, asegurando que un reinicio accidental o caída del navegador no provoque pérdida de datos.
