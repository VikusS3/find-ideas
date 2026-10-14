# Gestión de Riesgos, Estrategia de Distribución y Métricas

> **Documento:** 06 - Riesgos, Distribución y Métricas  
> **Fecha:** Octubre 2026  
> **Propósito:** Analizar los riesgos críticos identificados en el reporte de mercado, definir la estrategia Go-To-Market (GTM) y fijar las métricas clave de éxito (KPIs).

---

## 1. Matriz de Riesgos Críticos y Estrategias de Mitigación

El reporte de mercado destaca que la viabilidad técnica es alta, pero el éxito del proyecto depende de sortear 5 trampas estratégicas:

| Riesgo Identificado en Reporte | Severidad | Probabilidad | Mitigación Táctica en el Desarrollo |
| :--- | :--- | :--- | :--- |
| **1. Backlash anti-IA en comunidades de Game Dev** | Alta | Alta | **Nunca brandear como "AI Game Engine".** El posicionamiento oficial es *"Editor 2D ultraligero que corre en tu navegador y laptops modestas"*. La IA se presenta como un asistente opcional (Copilot) que puede desactivarse por completo. |
| **2. Competencia de gigantes y capital masivo** (Google Playground, Astrocade $56M) | Alta | Media | **Enfoque en Propiedad y Exportación Real.** Google y Astrocade crean jardines vallados para juegos casuales en navegador. Nuestro producto ofrece exportación limpia a itch.io, ejecutables nativos Tauri y código fuente abierto sin lock-in. |
| **3. Audiencia sensible al precio vs Coste de inferencia** | Media | Alta | **Arquitectura BYOK (Bring Your Own Key).** Al permitir que el usuario use sus propias credenciales de OpenAI/Claude/OpenRouter, el coste marginal de inferencia para nosotros es \$0. El free-tier de Cloudflare Workers AI se limita a la demo inicial. |
| **4. Trampa del Scope Creep (Sobrediseño del Editor)** | Crítica | Alta | **Regla de Alcance Rígido para el MVP:** Solo 2D con Phaser. Nada de 3D, nada de marketplace con pasarela de pagos ni fork complejo de Godot hasta validar retención y exportaciones. |
| **5. Cierre rápido de la ventana de oportunidad** | Media | Alta | **Ejecución en 12 semanas (MVP ágil).** Salir rápido al mercado con la combinación exacta de: Ligero + Assets CC0 + BYOK + Exportación libre. |

---

## 2. Estrategia de Distribución y Go-To-Market (GTM)

Dado que las palabras clave en Google Ads tienen un costo de adquisición inviable para un producto freemium/indie, la estrategia se basa en tres canales orgánicos de alta conversión:

```
+-----------------------------------------------------------------------------------+
|                        CANALES DE DISTRIBUCIÓN PRINCIPALES                        |
+-----------------------------------------------------------------------------------+
|  1. VIDEO-FIRST DEMOS (TikTok / YouTube Shorts / Reels)                           |
|     * Formato: "Haciendo un juego en 2 minutos en una laptop de $100 / Chromebook"|
|     * Hook: Sin instalar 15 GB de Unity, sin muros de créditos de IA.            |
|                                                                                   |
|  2. PARTICIPACIÓN EN GAME JAMS (itch.io / Ludum Dare)                             |
|     * Posicionamiento: La herramienta más rápida para prototipar en 48 horas.     |
|     * Plantillas preconfiguradas para temas comunes de jams.                      |
|                                                                                   |
|  3. COMUNIDADES INDIE Y FOROS TÉCNICOS                                            |
|     * Aportar valor técnico en r/aigamedev, r/indiedev y foros de Phaser.         |
|     * Publicaciones mostrando la arquitectura abierta y el soporte BYOK.          |
+-----------------------------------------------------------------------------------+
```

---

## 3. Plan de Validación Pre-Lanzamiento (Smoke Tests)

Antes de abrir el acceso general, se ejecutarán dos filtros de validación conductual:

### Test 1: Landing Page Smoke Test
- **Mensaje Principal:** *"Crea juegos 2D en tu navegador: ultraligero, corre en cualquier PC, con tu propia IA opcional y sin muros de créditos."*
- **Llamada a la Acción (CTA):** Registro para acceso anticipado a la beta privada.
- **Criterio de Éxito:** Tasa de conversión de visitantes únicos a emails registrados **> 10%**.

### Test 2: Prueba de Campo de Fricción Cero (5-10 Creadores)
- **Condición:** Sesión de 45 minutos en computadoras con procesadores modestos (4 GB RAM, sin GPU dedicada).
- **Misión del Tester:**
  1. Abrir el editor en el navegador y crear una escena desde cero o plantilla.
  2. Importar un asset de Kenney con 1 clic.
  3. Modificar la lógica con el asistente IA (vía BYOK o demo).
  4. Generar el archivo `.zip` y subirlo exitosamente a itch.io.
- **Criterio de Éxito:** Al menos el 80% de los testers completa el flujo sin asistencia del equipo de desarrollo.

---

## 4. Métricas Clave de Desempeño (KPIs)

### Métricas de Producto y Adopción
- **Tasa de Exportación (Export Rate):** Porcentaje de proyectos creados que generan al menos un build exportado (Meta: > 25%).
- **Retención D1 y D7:** Usuarios que regresan a editar su proyecto en 1 y 7 días (Meta D1: > 35%, Meta D7: > 18%).
- **Adopción de BYOK:** Porcentaje de usuarios activos que conectan su propia API Key (indica uso continuo y compromiso de power users).

### Métricas Técnicas y de Salud del Editor
- **Tasa de Caídas del Editor (Crash Rate):** < 0.1% de sesiones.
- **Tiempo de Inicio (Cold Start Time):** < 2.0 segundos en conexiones estándar.
- **Consumo Máximo de Memoria:** < 250 MB en modo edición y < 450 MB en modo simulación de juego.
- **Rendimiento de Renderizado:** Mínimo constante de 60 FPS en el canvas del editor sobre resoluciones 1080p.
