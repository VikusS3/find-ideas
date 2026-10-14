# Plan de Desarrollo: Editor de Videojuegos Ligero con IA Opcional

> **Documento:** 00 - Índice General y Resumen Ejecutivo  
> **Fecha:** Octubre 2026  
> **Origen:** Basado en la evaluación estratégica de `reports/plan-editor-ligero-ia.md`  
> **Estado:** Aprobado para Planificación de Ingeniería  

---

## 1. Visión del Producto

El proyecto consiste en el desarrollo de un **editor de videojuegos web-first y desktop ultraligero**, diseñado para operar con fluidez en hardware modesto (Chromebooks, laptops de 4 GB RAM) y sin barreras de instalación.

### Principios Rectores no Negociables
1. **El Editor es el Producto (100% Usable sin IA):** A diferencia de las plataformas "prompt-to-game" que atrapan al usuario en cajas negras, la herramienta es un motor y editor visual completo (escenas, nodos, física, lógica visual y scripting).
2. **IA como Asistente Opcional (Copiloto, no reemplazo):** La IA asiste bajo demanda del usuario mediante dos vías:
   - **Modo B (Asistente Contextual):** Generación de sprites, variación de audio, generación de snippets de script y sugerencias sobre entidades seleccionadas.
   - **Modo A (Generador Inicial):** Creación de un andamiaje base a partir de un prompt que se traduce directamente en el schema de proyecto editable.
3. **Cero Muros de Crédito Artificiales (BYOK First):** Soporte nativo para que el usuario conecte su propia API Key (OpenAI, Anthropic, OpenRouter, Cloudflare), eliminando el cobro abusivo de suscripciones por créditos de inferencia.
4. **Propiedad Real del Proyecto (Zero Lock-in):** Los proyectos se guardan en un formato abierto (`project.json`) y se exportan en 1-click a builds web limpios y autocontenidos listos para **itch.io**, ejecutables locales vía **Tauri** (<15 MB) o empaquetado móvil vía **Capacitor**.
5. **Catálogo de Assets CC0 Integrado:** Biblioteca local curada (Kenney, Quaternius, Poly Haven) con atribución de licencia automática en el build.

---

## 2. Mapa y Estructura de la Documentación

El plan de desarrollo se divide en 7 documentos modulares dentro de la carpeta `plan-desarrollo/`:

| Archivo | Enfoque | Audiencia |
| :--- | :--- | :--- |
| [00-indice-y-resumen-ejecutivo.md](file:///e:/Saul/Mis-Projectos/find-ideas/plan-desarrollo/00-indice-y-resumen-ejecutivo.md) | Visión general, scorecard, principios rectores y resumen del sistema. | Todos / Lead Dev |
| [01-arquitectura-y-stack.md](file:///e:/Saul/Mis-Projectos/find-ideas/plan-desarrollo/01-arquitectura-y-stack.md) | Stack técnico, Project JSON Schema v1, desacoplamiento Editor vs Runtime, State y Storage. | Arquitectura / Frontend |
| [02-especificacion-editor-core.md](file:///e:/Saul/Mis-Projectos/find-ideas/plan-desarrollo/02-especificacion-editor-core.md) | Viewport 2D, Scene Graph, Property Inspector, Visual Logic/Events, Monaco Editor y Playtest. | Core Dev / UI-UX |
| [03-sistema-ia-y-byok.md](file:///e:/Saul/Mis-Projectos/find-ideas/plan-desarrollo/03-sistema-ia-y-byok.md) | Workers AI, cliente BYOK local, Prompts estructurados, validación Zod y modos A/B. | AI Engineer / Backend |
| [04-assets-y-exportacion.md](file:///e:/Saul/Mis-Projectos/find-ideas/plan-desarrollo/04-assets-y-exportacion.md) | Gestor de Assets CC0, almacenamiento OPFS, pipeline de empaquetado Web (itch.io), Tauri y Capacitor. | Tooling / Build Ops |
| [05-plan-de-sprints-mvp.md](file:///e:/Saul/Mis-Projectos/find-ideas/plan-desarrollo/05-plan-de-sprints-mvp.md) | Cronograma táctico de 12 semanas (6 sprints de 2 semanas), tareas, DoDs e hitos. | Project Management |
| [06-riesgos-distribucion-y-metricas.md](file:///e:/Saul/Mis-Projectos/find-ideas/plan-desarrollo/06-riesgos-distribucion-y-metricas.md) | Mitigación del sentimiento anti-IA, estrategia Go-To-Market, smoke tests y métricas de rendimiento. | Growth / Product Owner |

---

## 3. Resumen del Alcance por Fases

```
+---------------------------------------------------------------------------------+
|                                 ROADMAP GLOBAL                                 |
+---------------------------------------------------------------------------------+
| FASE 1: MVP 2D (Semanas 1-12)                                                  |
|  * Editor 2D React/Solid + HTML5 Canvas con backend Phaser 3/4                 |
|  * Project JSON Schema v1 (Escenas, Nodos, Sprites, Colisionadores, Eventos)   |
|  * Gestor de Assets CC0 (Packs 2D Kenney) en IndexedDB / OPFS                  |
|  * Monaco Editor para scripting JS/TS ligero                                   |
|  * Asistente IA Modo B (BYOK + Cloudflare Workers AI beta)                     |
|  * Exportador 1-click a Web ZIP (HTML5 listo para itch.io)                     |
|  * Playtest instantáneo en iframe aislado sin recompilación                    |
+---------------------------------------------------------------------------------+
                                      |
                                      v
+---------------------------------------------------------------------------------+
| FASE 2: Expansión & Desktop (Meses 4-6)                                         |
|  * Modo A: Prompt-to-Game Schema scaffolding validado                          |
|  * Empaquetador de escritorio con Tauri (<15 MB instalador)                    |
|  * Integración 3D experimental con Three.js + Rapier physics                   |
|  * Shell móvil Android/iOS con Capacitor                                        |
|  * Importador web de texturas/modelos (Poly Haven API)                         |
+---------------------------------------------------------------------------------+
                                      |
                                      v
+---------------------------------------------------------------------------------+
| FASE 3: Ecosistema & Extensiones (Meses 7+)                                     |
|  * Exportador de interoperabilidad a proyecto Godot 4                           |
|  * Sistema de extensiones y plugins de la comunidad                             |
|  * Soporte WebGPU nativo para shaders personalizados                           |
+---------------------------------------------------------------------------------+
```

---

## 4. Presupuesto de Rendimiento y Huella Técnica

Para cumplir la promesa de "ultraligero que corre en computadoras modestas", se establecen los siguientes límites estrictos:
- **Consumo de Memoria RAM en Editor:** < 250 MB en reposo; < 450 MB durante playtest con assets.
- **Tiempo de Carga Inicial (First Contentful Paint):** < 1.8 segundos sobre conexión 4G / Wi-Fi estándar.
- **Peso de Descarga del Bundle Web:** < 3.5 MB gzip (incluyendo runtime core de Phaser y Monaco lazy-loaded).
- **Peso del Ejecutable Desktop (Tauri):** < 15 MB (Windows .msi / Linux AppImage / macOS .dmg).
- **Requisitos Mínimos:** Dual-core 1.8 GHz, 4 GB RAM, gráfica integrada con soporte WebGL 2.0.
