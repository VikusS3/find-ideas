# Especificación del Editor Core (Motor 2D)

> **Documento:** 02 - Especificación del Editor Core  
> **Fecha:** Octubre 2026  
> **Propósito:** Detallar los subsistemas visuales, el viewport de edición, la jerarquía de entidades, el sistema de lógica sin código y el entorno de scripting integrado.

---

## 1. Disposición Visual de la Interfaz (Layout del Editor)

La interfaz se inspira en el diseño ergonómico de herramientas modernas como Godot y Figma, optimizada para pantallas desde 13 pulgadas (1366x768) hasta monitores 4K.

```
+-----------------------------------------------------------------------------------------+
| [Logo] Proyecto: MiJuego2D  | [Escena 1 v] | [Undo] [Redo] |  [Play] [Pause] [Stop]     |
+---------------------+---------------------------------------------+---------------------+
| JERARQUÍA           | VIEWPORT CENTRAL                            | INSPECTOR           |
| (Scene Graph)       |                                             | (Propiedades)       |
|                     | [Grid 16px] [Snap: On] [Zoom: 150%]         |                     |
| > Nivel 1           |                                             | > Entidad: Jugador  |
|   v Mundo           |         +-----------------------+           |   Tag: Player       |
|     * Fondo         |         |  [Gizmo de Selección] |           |   Layer: Default    |
|     * Plataformas   |         |         /\            |           |                     |
|     v Jugador       |         |      <--[]-->         |           | v Transform         |
|       * Sprite      |         |         \/            |           |   X: 120   Y: 340   |
|       * Collider    |         +-----------------------+           |   Rot: 0   Scale: 1 |
|     * Enemigo_01    |                                             |                     |
|     * Moneda_A      |                                             | v SpriteRenderer    |
|                     |                                             |   Asset: hero.png   |
|                     |                                             |   Frame: 0          |
|                     |                                             |                     |
|                     |                                             | v ArcadeBody        |
|                     |                                             |   Gravity: Si       |
|                     |                                             |   Size: [28, 32]    |
+---------------------+---------------------------------------------+---------------------+
| ASSETS & EVENTOS (Pestañas inferiores)                                                  |
| [Packs CC0 Kenney]  [Mis Sprites]  [Audio]  [Eventos Visuales]  [Consola Debug]         |
|  [hero.png]  [tiles.png]  [coin.wav]  [jump.wav]  [+ Importar archivo / Drag & Drop]     |
+-----------------------------------------------------------------------------------------+
```

---

## 2. Subsistema de Viewport 2D y Manipulación

El Viewport central es un elemento HTML5 Canvas optimizado mediante WebGL2/Canvas2D que renderiza la vista de diseño del juego.

### 2.1 Capacidades de Navegación y Renderizado
- **Navegación Pan & Zoom:**
  - Pan: Clic con botón central o `Espacio + Arrastre de ratón`.
  - Zoom: Rueda de ratón (rango 10% a 800%) centrado en la posición del cursor.
- **Cuadrícula y Ajuste (Grid & Snapping):**
  - Cuadrículas preconfiguradas: 8x8, 16x16, 32x32 y 64x64 píxeles.
  - Snapping magnético activable/desactivable con tecla rápida `S`.
- **Modos de Renderizado de Vista:**
  - Modo Normal: Renderizado con texturas y colores finales.
  - Modo Wireframe / Colisionadores: Superposición de cajas de colisión (Hitboxes en verde/rojo).
  - Pixel-Art Filtering: `image-rendering: pixelated` para evitar interpolaciones borrosas en juegos retro.

### 2.2 Gizmos de Edición
- **Gizmo de Traslación:** Flechas cartesianas (Eje X rojo, Eje Y verde) con soporte de arrastre por eje o libre.
- **Gizmo de Escala y Rotación:** Manijas en las esquinas de la caja delimitadora (Bounding Box) con visualización de ángulo en tiempo real.
- **Edición de Polígonos de Colisión:** Edición visual de puntos de vértice arrastrables para definir colisionadores de formas irregulares.

---

## 3. Inspector de Propiedades Reactivo

El inspector renderiza dinámicamente controles según los componentes asociados a la entidad seleccionada:

### Componentes Base del MVP:
1. **TransformComponent:**
   - Posición (`x`, `y`), Rotación (grados/radianes), Escala (`scaleX`, `scaleY`), Profundidad de capa (`zIndex`).
2. **SpriteRendererComponent:**
   - Selector de asset (con vista previa en miniatura), Tint (color hexadecimal), Flip horizontal/vertical, Animación inicial.
3. **TilemapLayerComponent:**
   - Pincel de tilesets para pintar directamente sobre el viewport.
4. **ArcadeBodyComponent:**
   - Tipo de cuerpo (`dynamic` o `static`), Masa, Rebote (`bounce`), Fricción, Velocidad máxima, Activación de gravedad.
5. **CameraFollowComponent:**
   - Suavizado (lerp), Límites de cámara (bounds de escena), Offset respecto al objetivo.

---

## 4. Sistema de Lógica Visual (Eventos sin Código)

Para permitir que usuarios sin conocimientos de programación construyan mecánicas completas, el sistema adopta una arquitectura de **Gatillos y Acciones (Triggers & Actions)**:

```
+---------------------------------------------------------------------------+
| GATILLO (Trigger)              -> ACCIÓN (Action)                         |
+---------------------------------------------------------------------------+
| [Al Colisionar con "Moneda"]   -> 1. Sumar 10 a Variable "Puntaje"        |
|                                   2. Reproducir Sonido "coin.wav"         |
|                                   3. Destruir Objeto "Moneda"             |
+---------------------------------------------------------------------------+
| [Al Presionar Tecla "Espacio"] -> 1. Si "EnSuelo" == True:                |
|                                      Aplicar Impulso Y = -400             |
|                                      Reproducir Sonido "jump.wav"         |
+---------------------------------------------------------------------------+
| [Al Salir de Pantalla]         -> 1. Reiniciar Escena Actual              |
+---------------------------------------------------------------------------+
```

### Catálogo de Nodos de Lógica para el MVP:
- **Triggers:** `OnSceneStart`, `OnUpdate`, `OnCollisionEnter`, `OnTriggerEnter`, `OnKeyPressed`, `OnPointerDown`, `OnTimerTimeout`.
- **Condiciones:** `CompareVariable` (`==`, `!=`, `<`, `>`), `IsOnFloor`, `EntityExists`.
- **Acciones:** `SetPosition`, `ApplyVelocity`, `PlayAnimation`, `PlaySound`, `SpawnPrefab`, `DestroyEntity`, `ChangeScene`, `ModifyScore`.

---

## 5. Módulo de Scripting Avanzado con Monaco Editor

Para usuarios avanzados o cuando la lógica visual resulte insuficiente, se integra el editor **Monaco** embebido.

### 5.1 Ciclo de Vida del Script (Lifecycle Hook)
Los scripts siguen una interfaz TypeScript limpia y fuertemente tipada:

```typescript
import { BehaviorScript, Entity, EngineAPI } from '@light-engine/core';

export default class PlayerController implements BehaviorScript {
  public speed: number = 200;
  public jumpForce: number = 400;

  onInit(entity: Entity, api: EngineAPI): void {
    api.input.bindKey('ArrowLeft', () => entity.body.setVelocityX(-this.speed));
    api.input.bindKey('ArrowRight', () => entity.body.setVelocityX(this.speed));
    api.input.bindKey('Space', () => {
      if (entity.body.blocked.down) {
        entity.body.setVelocityY(-this.jumpForce);
        api.audio.play('jump');
      }
    });
  }

  onUpdate(entity: Entity, dt: number, api: EngineAPI): void {
    if (!api.input.isDown('ArrowLeft') && !api.input.isDown('ArrowRight')) {
      entity.body.setVelocityX(0);
    }
  }

  onDestroy(entity: Entity, api: EngineAPI): void {
    // Limpieza de suscripciones
  }
}
```

### 5.2 Autocompletado y Tipado Dinámico
- El editor genera en tiempo real un archivo virtual `project-types.d.ts` que contiene los nombres exactos de todas las entidades, tags, escenas y assets registrados en el schema del proyecto, permitiendo IntelliSense contextual.

---

## 6. Subsistema de Playtest Instantáneo

1. **Clonado de Estado en Memoria:**
   - Antes de iniciar la simulación, el store genera una copia serializada inmutable del `project.json`.
2. **Ejecución en Sandbox:**
   - El IFrame del runtime inicializa la escena de juego. No requiere empaquetado en disco ni transpilaciones pesadas (se usa sucrase/esbuild en navegador para transformar TypeScript a JavaScript estándar en <20ms).
3. **Reversión Perfecta al Detener:**
   - Al pulsar `Stop`, se destruye la instancia viva de Phaser en el iframe y se restaura el árbol de entidades al estado exacto previo a la prueba.
