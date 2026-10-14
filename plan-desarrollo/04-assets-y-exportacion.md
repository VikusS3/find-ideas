# Módulo de Assets CC0 y Pipeline de Exportación

> **Documento:** 04 - Módulo de Assets y Exportación  
> **Fecha:** Octubre 2026  
> **Propósito:** Definir el catálogo local de assets CC0, la persistencia en almacenamiento local del navegador y la arquitectura de exportación multiplataforma (Web/itch.io, Desktop Tauri y Móvil Capacitor).

---

## 1. Módulo de Assets CC0 Integrado

Uno de los mayores dolores para desarrolladores principiantes y creadores en hardware modesto es encontrar recursos gráficos y sonoros utilizables de forma legal sin salir del editor ni pagar suscripciones de stock.

```
+-----------------------------------------------------------------------------------+
|                        EXPLORADOR DE ASSETS CURADOS CC0                           |
+-----------------------------------------------------------------------------------+
| Categorías: [Todos]  [Sprites 2D]  [Tilesets]  [Efectos de Audio]  [UI & Fuentes]  |
|                                                                                   |
| +-----------------+  +-----------------+  +-----------------+  +----------------+ |
| | [Miniatura]     |  | [Miniatura]     |  | [Miniatura]     |  | [Miniatura]    | |
| | Kenney Platform |  | Kenney Roguelike|  | Kenney Retro Sfx|  | Kenney UI Pack | |
| | Formato: PNG    |  | Formato: PNG    |  | Formato: WAV    |  | Formato: PNG   | |
| | Licencia: CC0   |  | Licencia: CC0   |  | Licencia: CC0   |  | Licencia: CC0  | |
| | [Importar 1-Clk]|  | [Importar 1-Clk]|  | [Importar 1-Clk]|  | [Importar 1-Clk| |
| +-----------------+  +-----------------+  +-----------------+  +----------------+ |
+-----------------------------------------------------------------------------------+
```

### 1.1 Proveedores y Fuentes Seleccionadas para el MVP:
- **Kenney.nl (Packs 2D Base):** Sprites de plataformas, tilesets ortogonales (16x16 y 32x32), elementos de interfaz y efectos de sonido de 8 bits sintetizados. Licencia CC0 (Dominio Público).
- **Quaternius (Fase 2 - 3D):** Modelos low-poly optimizados en formato estándar **glTF / GLB** con rigs básicos. Licencia CC0.
- **Poly Haven (Fase 2 - Texturas):** Materiales PBR y mapas HDRI ligeros. Licencia CC0.

### 1.2 Pipeline de Almacenamiento Local (Local-First):
- **Cero Dependencia de Servidores:** Los paquetes esenciales se sirven mediante caché HTTP en la primera visita y se almacenan permanentemente en el navegador utilizando **OPFS (Origin Private File System)** o **IndexedDB (idb-keyval)**.
- **Carga sin Lag:** Al arrastrar un sprite desde el navegador de assets al Viewport, el asset se referencia por su ID único sin incurrir en peticiones de red adicionales.
- **Trazabilidad Legal:** Cada asset importado registra su metadato de licencia en el `project.json` y genera automáticamente el archivo `LICENSES.txt` durante la exportación final.

---

## 2. Pipeline de Exportación Web (1-Click para itch.io)

El objetivo primario de exportación del MVP es la web independiente (itch.io, Newgrounds, GameJolt o alojamiento estático propio).

```
[ Proyecto en Editor: project.json + Scripts + Assets ]
                          |
                          v
         [ Generador de Build (In-Browser / WebWorker) ]
         - Transpila BehaviorScripts con Sucrase/ESBuild a ES6
         - Empaqueta el runtime ligero de Phaser (~1 MB minificado)
         - Genera el HTML de arranque autocontenido
         - Comprime assets y genera archivo `LICENSES.txt`
                          |
                          v
                [ Archivo .ZIP Listo ]
                |-- index.html
                |-- game.js
                |-- project-data.json
                |-- assets/
                |   |-- hero.png
                |   |-- sfx.wav
                `-- LICENSES.txt
```

### Características del Build Web:
1. **Cero Dependencias Externas (Offline Ready):** No carga CDNs en tiempo de ejecución. El juego puede abrirse haciendo doble clic en el archivo local o subirse directamente a itch.io marcando *"This file will be played in the browser"*.
2. **Auto-Escalado Responsive:** Soporte de diferentes relaciones de aspecto (16:9, 4:3, responsive letterboxing) para adaptarse a pantallas móviles o monitores de escritorio.
3. **Carga Ultrarrápida:** El tamaño total de un juego 2D básico promedio con este pipeline es inferior a **2.5 MB** comprimido.

---

## 3. Pipeline de Exportación Desktop con Tauri 2.0

Para usuarios que desean distribuir ejecutables nativos en Steam o itch.io sin obligar a los jugadores a descargar los 200 MB de Electron:

```
+-----------------------------------------------------------------------------------+
|                              ARQUITECTURA TAURI                                   |
|                                                                                   |
|  +-----------------------------------------------------------------------------+  |
|  | Contenedor Nativo Ligero en Rust (~5-12 MB)                                 |  |
|  | (Manejo de archivos de guardado local, pantalla completa nativa, gamepad)   |  |
|  +-----------------------------------------------------------------------------+  |
|                                        |                                          |
|                                        v                                          |
|  +-----------------------------------------------------------------------------+  |
|  | WebView Nativo del Sistema Operativo                                        |  |
|  | - Windows: Microsoft Edge WebView2 (preinstalado en Windows 10/11)          |  |
|  | - macOS: WebKit nativo                                                      |  |
|  | - Linux: WebKitGTK                                                          |  |
|  +-----------------------------------------------------------------------------+  |
+-----------------------------------------------------------------------------------+
```

### Ventajas Técnicas:
- **Huella de Memoria Mínima:** En reposo, una aplicación Tauri consume típicamente entre 35 y 70 MB de RAM, comparado con los 300-500 MB habituales de Electron.
- **Empaquetado Multiplataforma:** Generación de instaladores `.msi`/`.exe` para Windows, `.dmg` para macOS y `.AppImage`/`.deb` para Linux.

---

## 4. Pipeline de Exportación Móvil con Capacitor 6

Permite transformar el bundle web en un proyecto nativo de Android Studio o Xcode:
- **Capa Híbrida Optimizada:** Utiliza Android System WebView y iOS WKWebView configurados en modo acelerado por hardware WebGL.
- **Soporte de Controles Táctiles (Virtual D-Pad & Joysticks):** Inyección automática de controles táctiles en pantalla si se detecta un entorno móvil.
- **Cumplimiento de Políticas de Tienda:** Conforme a la directriz 4.7 de Apple y políticas de Google Play, los juegos HTML5 empaquetados como aplicaciones independientes son aprobables siempre que no intenten desplegar una tienda secundaria de descarga dentro de la app.
