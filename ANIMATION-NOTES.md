# 🎬 Banner Animado — Notas de esta versión

## Qué hace

Loop de **14.2s** que arranca con un intro de 3.2s (una sola vez al cargar), y luego repite:

`Retrato (3.0s) → transición (1.3s) → React (2.0s) → transición (1.3s) → TypeScript (2.0s) → transición (1.3s) → JavaScript (2.0s) → transición (1.3s) → vuelve a Retrato`

- **Intro:** las 94 "bandas" del retrato aparecen en orden aleatorio y disperso (no de arriba a abajo, no por región) — se nota como un shimmer que se arma solo.
- **Retrato → logos:** el retrato se atenúa (no desaparece del todo) y sus 94 bandas se desplazan ~42% hacia el centro de React, con ruido aleatorio por banda para que no se vea como una cuadrícula.
- **Logos:** 700 puntos "viajeros" (React → TypeScript → JavaScript) emparejados por transporte óptimo (`scipy.optimize.linear_sum_assignment`) para que cada punto recorra la distancia más corta — sin cruces caóticos.
- Los 3 logos son los trazos oficiales de **simple-icons** (paquete MIT, hecho justo para esto — no son dibujados a mano).

## Peso real

**~960KB por archivo** (`dark.svg` / `light.svg`). Esto es exactamente lo que tu propio PDF anticipa
("Banner files land ~900KB–1MB. Warn me before expensive changes") — no es un error, es el costo real
de tener 94 bandas de retrato + 700 puntos viajeros animados independientemente. Antes de esto ya
habíamos pasado por versiones de 1.4MB y 178KB; este es el punto donde vive la versión "completa" que
pediste.

## Cómo lo verifiqué (sin poder verlo animado yo mismo)

No tengo navegador para reproducir SMIL en vivo, así que en vez de confiar en una vista previa estática
(que solo muestra el frame inicial, como tu propio PDF advierte sobre `cairosvg`), **recalculé manualmente
la interpolación de cada keyframe en Python** y rendericé 6 fotogramas en los momentos clave del loop
(intro, transición a React, React sostenido, transición a TypeScript, JavaScript sostenido, transición de
vuelta). Los 6 se ven correctos: el retrato se dispersa de forma pareja (no por parches), los logos se
forman reconociblemente, y las transiciones interpolan sin saltos. Aun así, **la validación final la
tienes que hacer tú en el navegador** — abre el SVG directamente o mira tu perfil en GitHub.

## Soporte de SMIL en GitHub

Las animaciones SVG (`<animate>`, `<animateTransform>`) sí funcionan en Chrome, Firefox y Safari cuando
el SVG se carga como `<img>` — a diferencia de `foreignObject`, que es justamente lo que rompía las
versiones anteriores. Esto es una técnica muy usada (typing-svg, contadores animados, etc.) y estable.

## Si el resultado no te convence

Como bien pedía tu PDF: si algo no te gusta, dímelo con lo específico (¿muy tenue el retrato durante los
logos? ¿quieres otro orden de logos? ¿los puntos viajeros muy dispersos?) y ajusto los parámetros — no
hace falta regenerar todo el pipeline desde cero, son números puntuales en el script.
