# Sistema de IA y Arquitectura BYOK (Bring Your Own Key)

> **Documento:** 03 - Sistema de IA y BYOK  
> **Fecha:** Octubre 2026  
> **Propósito:** Especificar la integración de inteligencia artificial opcional, la arquitectura cliente directa para BYOK y la validación de schemas de proyecto.

---

## 1. Filosofía de la Capa de IA

Para evitar el rechazo comunitario evidenciado en el market research (52% de los desarrolladores expresan rechazo al branding de "motor de IA"), el sistema opera bajo los siguientes axiomas:

1. **La IA es un Asistente, no el Conductor:** El editor funciona al 100% con las funcionalidades de IA deshabilitadas o desconectadas. No existen bloqueos que exijan usar IA.
2. **Cero Muros de Crédito Propietarios:** A diferencia de Unity AI o Rosebud (que cobran planes mensuales de $10-$100 que se agotan rápidamente), los usuarios pueden operar con su propia clave de API (**BYOK**).
3. **Generación hacia Estándares Abiertos:** Cualquier salida de IA se traduce en código TypeScript limpio o en el schema abierto `project.json`. Nunca se genera código ofuscado o atado a un backend cerrado.

---

## 2. Modos de Operación de la IA

```
                              +---------------------------------------+
                              |        INTERFAZ DEL ASISTENTE         |
                              +---------------------------------------+
                                           /             \
                                          /               \
                                         v                 v
                 +-------------------------------+   +-------------------------------+
                 |  MODO A: Generador Inicial    |   |  MODO B: Asistente Contextual |
                 |  (Prompt -> Proyecto Schema)  |   |  (Sobre Selección de Entidad) |
                 +---------------+---------------+   +---------------+---------------+
                                 |                                   |
                                 v                                   v
                 +-------------------------------+   +-------------------------------+
                 | LLM emite `project-v1.json`   |   | Operaciones Puntuales:        |
                 | Validador Zod / JSON Schema   |   | 1. Generar Sprite (Flux)      |
                 | Carga directa en el editor    |   | 2. Escribir Behavior Script   |
                 | para edición visual manual    |   | 3. Ajustar física/componentes |
                 +-------------------------------+   +-------------------------------+
```

### 2.1 Modo B: Asistente Contextual (Enfoque Prioritario en MVP)
Opera sobre la entidad o contexto seleccionado en el editor:
- **Generación de Assets 2D (Sprites):** El usuario pulsa sobre un slot de sprite y escribe *"caballero pixel-art con espada en pose idle"*. El asistente llama a un modelo de difusión (`flux-1-schnell`), remueve el fondo automáticamente vía canvas post-processing y lo asigna al `SpriteRenderer`.
- **Generación de Comportamiento:** El usuario selecciona la entidad *"Enemigo"* y solicita *"crea una patrulla horizontal que cambie de dirección al tocar una pared"*. La IA emite un script de comportamiento TypeScript que se vincula directamente a la entidad.
- **Modificación de Propiedades:** Instrucciones en lenguaje natural como *"haz que este personaje salte el doble de alto y tenga menos gravedad"* modifican directamente los valores numéricos del componente `ArcadeBody` en el inspector.

### 2.2 Modo A: Generador de Andamiaje Inicial (Scaffolder)
- Transforma un concepto general (ej. *"un juego estilo Flappy Bird submarino con obstáculos de coral y burbujas que dan puntos"*) en una estructura válida de `project.json`.
- El resultado se inyecta en el canvas del editor: todas las entidades, colisionadores y eventos quedan expuestos en el árbol de jerarquía para que el usuario pueda modificarlos a mano inmediatamente.

---

## 3. Catálogo de Modelos y Proveedores

El editor ofrece dos vías de inferencia:

### Vía 1: Cloudflare Workers AI (Entorno Demo / Beta Gratuita)
Utilizado para la experiencia "out-of-the-box" sin configuración inicial:
- **Cuota Gratuita:** 10,000 neuronas diarias por proyecto (~100-140 consultas de lógica ligeras al día).
- **Modelos Seleccionados:**
  - Lógica rápida y scripts: `@cf/qwen/qwen3-30b-a3b-fp8` o `@cf/zai-org/glm-4.7-flash`.
  - Generación de Sprites 2D: `@cf/black-forest-labs/flux-1-schnell` (rápido, ~4 pasos) y `flux-2-klein-9b`.
  - Emisión de Schema JSON: `@cf/meta/llama-3.3-70b-instruct-fp8-fast` con modo JSON activado.

### Vía 2: Arquitectura BYOK (Bring Your Own Key) Directa
El usuario introduce su propia API Key en el panel de configuración:
- **Proveedores Soportados:**
  - **OpenAI:** GPT-4o, GPT-4o-mini (excelente para estructurar JSON con Structured Outputs).
  - **Anthropic:** Claude 3.5 Sonnet (estándar de la industria para generación de código TypeScript de alta fidelidad).
  - **OpenRouter / DeepSeek:** DeepSeek-V3 y DeepSeek-Coder (coste de inferencia extremadamente económico para usuarios indie).
- **Seguridad y Privacidad:**
  - Las llaves de API se guardan exclusivamente en el almacenamiento local del navegador (`localStorage` cifrado o memoria de sesión) o en el keystore del sistema operativo en la versión Tauri.
  - Las peticiones HTTP viajan directamente desde el cliente del usuario hacia los endpoints oficiales de cada proveedor, **sin servidores intermediarios nuestros**. Cero riesgo de fugas de credenciales en nuestra infraestructura.

---

## 4. Pipeline de Validación de Salidas JSON con Zod

La generación de esquemas de juego por parte de LLMs es propensa a alucinaciones de formato. Para garantizar que ningún JSON inválido corrompa el proyecto:

```typescript
import { z } from 'zod';

// Esquema de Validación del Proyecto
export const EntitySchema = z.object({
  id: z.string(),
  name: z.string(),
  tag: z.string().default('Untagged'),
  transform: z.object({
    position: z.object({ x: z.number(), y: z.number() }),
    rotation: z.number().default(0),
    scale: z.object({ x: z.number(), y: z.number() }).default({ x: 1, y: 1 })
  }),
  components: z.array(z.object({
    type: z.string(),
    properties: z.record(z.any())
  }))
});

export const ProjectSchemaValidator = z.object({
  version: z.literal('1.0.0'),
  engine: z.literal('phaser-2d'),
  canvas: z.object({
    width: z.number().int().positive(),
    height: z.number().int().positive(),
    pixelArt: z.boolean().default(true)
  }),
  scenes: z.array(z.object({
    id: z.string(),
    name: z.string(),
    entities: z.array(EntitySchema)
  }))
});
```

### Protocolo de Auto-Corrección:
1. Si la salida del LLM no pasa la validación de Zod, se captura la lista de errores exactos (`error.issues`).
2. Se envía un segundo mensaje automático al modelo indicando:
   > *"Tu JSON anterior falló con los siguientes errores de validación: [Lista de errores]. Corrige únicamente esos campos y devuelve el JSON válido."*
3. Tasa de éxito tras 1 reintento: >96% en pruebas con modelos de la familia Llama 3.3 / Claude 3.5.

---

## 5. System Prompt Maestro para el Asistente

```markdown
Eres el Asistente de Ingeniería de Juego para LightEngine 2D.
Tu misión es asistir al usuario generando componentes, assets y scripts TypeScript limpios y eficientes.

Reglas Obligatorias:
1. No inventes APIs ajenas a Phaser 3 / LightEngine Core.
2. Si generas un script de comportamiento, implementa siempre la interfaz `BehaviorScript` con hooks `onInit`, `onUpdate` y `onDestroy`.
3. Nunca añadas dependencias de NPM externas en el código generado.
4. Mantén la lógica simple, legible y libre de memoria residual (limpia timers y eventos en `onDestroy`).
5. Cuando devuelvas esquemas de proyecto o modificaciones de entidades, emite únicamente JSON puro sin bloques de texto conversacional innecesarios.
```
