# 📋 Guía de Configuración del Perfil

## ✅ Estado Actual

### Archivos Actualizados
- ✅ `README.md` — secciones en español, rutas de assets verificadas
- ✅ `assets/dark.svg` y `assets/light.svg` — banner reconstruido en SVG puro, ~6.4KB c/u (antes 864KB–1.4MB)
- ✅ `assets/stack.svg` y `assets/quests.svg` — reconstruidos en SVG puro (antes usaban `foreignObject`, por eso no se veían)
- ✅ `.github/workflows/snake.yml` — sin cambios, ya estaba bien configurado

### Información Personal (ya aplicada en los assets, no solo en el texto del README)
- 📍 Origin: Barquisimeto, Venezuela
- 🎓 Education: Analista de Sistemas (En Progreso)
- 🌐 Grid.Portfolio: portafolio-indol-eight.vercel.app
- 📧 Grid.Mail: mendozadavidprogramacion2.0@gmail.com
- 🚫 Grid.LinkedIn / Grid.Facebook: eliminados del banner (ya no aparecen como campos "por completar")

## 🐛 Causa raíz de los problemas anteriores

1. **Tech Stack y Top Languages "invisibles":**
   - Top Languages / GitHub Stats (tabla de arriba) son imágenes externas de `github-readme-stats.vercel.app` — funcionan normalmente, solo pueden tardar unos segundos en cargar la primera vez.
   - `stack.svg` y `quests.svg` (Tech Stack y Proyectos) **sí estaban realmente rotos**: usaban `<foreignObject>` con HTML/CSS interno. Los navegadores no renderizan ese contenido cuando el SVG se carga como `<img>` (que es como GitHub los muestra), así que aparecían en blanco. Se reconstruyeron con SVG puro (rect/text/line), sin esa dependencia.

2. **Campos sin completar en el banner:**
   - El banner tenía literalmente el texto `— agrega tu ciudad —`, `— agrega tu carrera —`, `— agrega tu portfolio —`, `— agrega tu LinkedIn —`, `— agrega tu Facebook —` dentro del SVG. Ya están reemplazados con tus datos reales, y las filas de LinkedIn/Facebook se eliminaron por completo.

## 🔧 Pasos para publicar estos cambios

Como este chat no tiene acceso de escritura a tu repositorio de GitHub, sube los archivos manualmente:

1. Descarga los archivos entregados (`README.md`, `CLAUDE.md`, `CHECKLIST.md`, y la carpeta `assets/` con `dark.svg`, `light.svg`, `stack.svg`, `quests.svg`).
2. En GitHub, entra a `MendozaDavidprogam/MendozaDavidprogam`.
3. Reemplaza cada archivo (Add file → Upload files, o edítalos uno por uno) manteniendo la misma estructura de carpetas (`assets/...`).
4. Confirma el commit en `main`.
5. Espera 1–2 minutos y refresca tu perfil (agrega `?v=1` a la URL si el caché de GitHub tarda en actualizar).

## ✅ Verificación

- El workflow del snake ya tiene una ejecución exitosa en la rama `output` — no requiere acción.
- Las estadísticas (`github-readme-stats.vercel.app`) no requieren token ni configuración adicional.
