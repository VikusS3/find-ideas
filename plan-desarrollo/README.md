# Plan de Desarrollo: Editor de Videojuegos Ligero con IA Opcional

Este directorio contiene la documentación técnica, arquitectónica y el plan de ejecución táctico derivado del análisis y evaluación estratégica del reporte [`reports/plan-editor-ligero-ia.md`](../reports/plan-editor-ligero-ia.md).

## Estructura de Documentación

1. **[00-indice-y-resumen-ejecutivo.md](00-indice-y-resumen-ejecutivo.md)**  
   Visión general del producto, principios rectores no negociables, scorecard del pivot y presupuestos de rendimiento.
2. **[01-arquitectura-y-stack.md](01-arquitectura-y-stack.md)**  
   Stack tecnológico seleccionado, desacoplamiento Editor vs. Runtime (IFrame Sandbox), especificación del `project-v1.json` y gestión de estado con Undo/Redo (Zustand + OPFS).
3. **[02-especificacion-editor-core.md](02-especificacion-editor-core.md)**  
   Layout de la interfaz, Viewport 2D con Gizmos y Snapping, Inspector reactivo de propiedades, Sistema de Lógica Visual (Triggers & Actions), Monaco Editor y Playtest instantáneo.
4. **[03-sistema-ia-y-byok.md](03-sistema-ia-y-byok.md)**  
   Filosofía de IA opcional, Modos A (Scaffolder) y B (Asistente contextual), integración con Cloudflare Workers AI, arquitectura cliente BYOK y auto-corrección de JSON con Zod.
5. **[04-assets-y-exportacion.md](04-assets-y-exportacion.md)**  
   Módulo de Assets CC0 locales (Kenney, Quaternius, Poly Haven), persistencia local-first y pipelines de exportación multiplataforma (Web/itch.io ZIP, Desktop Tauri y Móvil Capacitor).
6. **[05-plan-de-sprints-mvp.md](05-plan-de-sprints-mvp.md)**  
   Cronograma de desarrollo de 12 semanas (6 sprints de 2 semanas) con metas, entregables, criterios de aceptación (DoD) y asignación para 1-2 ingenieros.
7. **[06-riesgos-distribucion-y-metricas.md](06-riesgos-distribucion-y-metricas.md)**  
   Matriz de mitigación de riesgos (anti-IA branding, competencia de gigantes, costes de inferencia), estrategia GTM video-first, smoke-tests y KPIs de producto.
