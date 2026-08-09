# 🎬 Banner Animado — versión GIF (definitiva)

## Por qué se cambió de SVG animado a GIF

Confirmado con varias fuentes: **GitHub elimina las etiquetas `<animate>` / `<animateTransform>`
de cualquier SVG que se muestre en un README** (vía `<img>` o `![]()`), como medida de seguridad
contra XSS (una animación SVG puede usarse para ejecutar JavaScript disfrazado). No es un límite de
rendimiento ni de cuántos elementos tenga el archivo — es un filtro que corre en el servidor de
GitHub antes de que el navegador reciba el archivo. Por eso, sin importar cuánto se optimizara el
SVG, nunca se iba a mover en tu perfil real.

Esto no se puede evitar dentro de un SVG. La única forma de tener animación real en un README de
GitHub es con un **GIF animado** (o video/APNG, pero GIF es lo estándar y lo que usa la inmensa
mayoría de perfiles animados en GitHub) — porque un GIF no depende de scripts ni de SMIL, son
fotogramas planos, y GitHub sí los reproduce tal cual.

## Qué contiene

Mismo diseño y mismo timeline de siempre (recalculado matemáticamente, no simulado a ojo):
**retrato → React → TypeScript → JavaScript → retrato**, en loop continuo.

- 90 fotogramas por tema, comprimidos a 27 únicos donde el contenido no cambiaba (GIF optimiza
  automáticamente los tramos de "hold").
- `dark.gif`: ~740KB · `light.gif`: ~1.03MB.
- Mismo recorte ampliado de la ronda anterior (más aire arriba del pelo y a los lados).

## Verificación

Extraje fotogramas reales del GIF ya generado (no una simulación aparte) en varios puntos del loop
y confirmé visualmente: el retrato se ve completo con margen, se disuelve, el logo de React se
forma reconocible, migra a TypeScript, luego a JavaScript, y vuelve al retrato — todo fluido porque
ahora es un GIF de verdad, no SMIL bloqueado por GitHub.

## Un par de notas honestas

- El GIF no se ve tan nítido como un SVG a cualquier zoom (SVG es vectorial, GIF es raster a
  1180px de ancho) — a tamaño normal de README no se nota, pero si alguien hace zoom se pixela.
- `<picture>` con `<source>` sigue funcionando igual para alternar dark/light — el mecanismo no
  depende del formato de imagen.
- `stack.svg`, `quests.svg` y `stats.svg` no cambian — nunca tuvieron animación, así que no les
  afecta esta limitación de GitHub.
