# Plan de Sprints y Ejecución Táctica (MVP de 12 Semanas)

> **Documento:** 05 - Plan de Sprints MVP  
> **Fecha:** Octubre 2026  
> **Equipo Estimado:** 1 - 2 Ingenieros Fullstack / Game Dev  
> **Duración Total:** 12 Semanas (6 Sprints de 2 semanas)

---

## 1. Cronograma General de Sprints

```
Semana:   01  02 | 03  04 | 05  06 | 07  08 | 09  10 | 11  12
Sprint:  [  S1  ] [  S2  ] [  S3  ] [  S4  ] [  S5  ] [  S6  ]
Fase:    Cimiento | Viewport| Runtime| Script |   IA   | Export
                  |  Gizmos | Eventos| Assets |  BYOK  |   Beta
```

---

## 2. Desglose Detallado por Sprint

### Sprint 1 (Semanas 1 - 2): Fundaciones del Sistema y Project Schema
- **Objetivos:**
  1. Configuración del monorepo Vite + React 19 + TypeScript + Tailwind CSS.
  2. Implementación formal del `project-v1.json` con validadores **Zod**.
  3. Store central con **Zustand** e historial de comandos (Undo/Redo base con 50 pasos).
  4. Capa de almacenamiento local-first con **OPFS (Origin Private File System)** y auto-guardado cada 3 segundos.
- **Entregables:**
  - El editor carga y guarda proyectos en memoria y en disco local sin caídas.
  - Pruebas unitarias de serialización/deserialización del schema con 100% de cobertura.
- **Criterio de Aceptación (DoD):**
  - Un archivo JSON modificado manualmente se recarga en <100ms y valida su integridad.

---

### Sprint 2 (Semanas 3 - 4): Viewport 2D, Gizmos y Árbol de Jerarquía
- **Objetivos:**
  1. Renderizado del Canvas 2D interactivo con pan, zoom (10%-800%) y cuadrícula magnética (8/16/32px).
  2. Implementación de Gizmos visuales de traslación, escala y bounding boxes de selección.
  3. Panel de Jerarquía (Scene Graph) con soporte de selección múltiple, reordenamiento y borrado de entidades.
  4. Inspector básico de componentes: `TransformComponent`, `TagComponent`.
- **Entregables:**
  - Creación, movimiento y eliminación visual de entidades en el canvas con feedback fluido a 60 FPS.
- **Criterio de Aceptación (DoD):**
  - El usuario puede colocar 50 entidades en escena con un uso de memoria inferior a 120 MB de RAM.

---

### Sprint 3 (Semanas 5 - 6): Puente de Runtime Phaser y Lógica Visual (No-Code)
- **Objetivos:**
  1. Iframe sandbox para el runtime de Phaser 3/4 desacoplado del hilo principal del editor.
  2. Sistema de sincronización de escenas mediante mensajes tipados (`postMessage`).
  3. Modo Playtest instantáneo con clonado inmutable de estado (F5 / botón Play) y reinicio limpio.
  4. Editor de eventos visuales (Gatillos y Acciones: colisiones, pulsación de teclas, variables simples).
- **Entregables:**
  - Un prototipo jugable de plataformas o arcade ejecutable y comprobable dentro del editor.
- **Criterio de Aceptación (DoD):**
  - La transición de "Edición" a "Playtest" ocurre en menos de 300 milisegundos.

---

### Sprint 4 (Semanas 7 - 8): Monaco Scripting y Catálogo de Assets CC0
- **Objetivos:**
  1. Integración de **Monaco Editor** embebido con carga diferida (lazy load).
  2. Generador dinámico de definiciones TypeScript (`d.ts`) contextuales a la escena.
  3. Transpilador en navegador con **Sucrase** para convertir scripts a JS en <15ms.
  4. Explorador de Assets CC0 locales con packs 2D de **Kenney** (Sprites, tilesets, SFX).
  5. Asignación mediante Drag & Drop desde el estante de assets hacia las entidades del viewport.
- **Entregables:**
  - Posibilidad de programar mecánicas complejas mediante código TypeScript con autocompletado y usar assets con licencia CC0 integrada.
- **Criterio de Aceptación (DoD):**
  - Monaco no degrada los FPS del editor cuando el panel de código está oculto.

---

### Sprint 5 (Semanas 9 - 10): Módulo de IA Asistente (Modo B) y BYOK
- **Objetivos:**
  1. Panel lateral del asistente IA con arquitectura cliente para **BYOK** (OpenAI, Anthropic, OpenRouter).
  2. Integración del backend beta con **Cloudflare Workers AI** (Qwen3-30b y Flux-1-schnell).
  3. Modo B sobre entidad seleccionada: generación de sprites con eliminación de fondo y generación de snippets de script.
  4. Ciclo de auto-corrección de JSON guiado por el validador Zod.
- **Entregables:**
  - Un usuario puede pulsar un botón para solicitar un sprite o un script de movimiento y verlo aplicado directamente en la entidad activa sin recargar el editor.
- **Criterio de Aceptación (DoD):**
  - Si el usuario no introduce una API key o apaga la IA, la interfaz no muestra advertencias ni bloqueos funcionales.

---

### Sprint 6 (Semanas 11 - 12): Exportador Web (itch.io), QA en Hardware Modesto y Beta
- **Objetivos:**
  1. Generador de archivos ZIP para exportación web limpia (autocontenida, offline-ready).
  2. Generador automático de `LICENSES.txt` con atribuciones CC0.
  3. Pruebas de rendimiento y optimización en hardware modesto (laptop con 4 GB RAM / procesador Celeron o i3).
  4. Despliegue de la landing page con smoke-test y apertura del formulario de beta cerrada.
- **Entregables:**
  - Build funcional del editor desplegado en la web.
  - Juego de demostración exportado y alojado exitosamente en itch.io.
- **Criterio de Aceptación (DoD):**
  - El test de campo (§7 del reporte): un betatester en PC modesto crea un juego 2D, usa un asset CC0, añade un script y exporta a itch.io en una única sesión fluida.

---

## 3. Matriz de Responsabilidades Típica (Equipo de 2 Desarrolladores)

| Rol | Foco Principal | Sprints Clave |
| :--- | :--- | :--- |
| **Dev A (Core & Engine)** | Arquitectura de estado, Viewport, Gizmos, Bridge con Phaser, Exportador ZIP. | S1, S2, S3, S6 |
| **Dev B (Tooling & AI)** | Inspector UI, Integración de Monaco, Browser de Assets CC0, Integración BYOK/Workers AI. | S2, S4, S5, S6 |
