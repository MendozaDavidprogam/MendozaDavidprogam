# Checklist de despliegue

## Archivos entregados
- `assets/dark.svg` y `assets/light.svg` → tu banner animado (retrato con dithering + morph de logos React/Node/`</>`)
- `README.md` → listo para pegar en tu repo `MendozaDavidprogam/MendozaDavidprogam`
- `snake.yml` → workflow del snake de contribuciones

## Pasos manuales (en orden)

1. **Sube los SVG del banner**
   Repo → `assets/` → Add file → Upload files → sube `dark.svg` y `light.svg` (no reemplaces `stack.svg` ni `quests.svg`, esos ya los tienes).

2. **Reemplaza tu README.md**
   Pega el contenido del `README.md` entregado en la raíz de tu repo.

3. **Auto-aloja las stats (evita el "API rate limit exceeded")**
   - `github.com/settings/tokens` → Tokens (classic) → Generate new (classic) → scope `repo` → sin expiración → copia el token (solo se muestra una vez, nunca lo pegues en ningún chat ni repo público)
   - Fork de `anuraghazra/github-readme-stats`
   - `vercel.com` → sign up con GitHub → plan Hobby (gratis) → Add New → Project → importa tu fork
   - Environment Variables → `PAT_1` = tu token → Deploy
   - Copia tu URL (`algo.vercel.app`) y reemplaza **todas** las apariciones de `YOUR-INSTANCE` en el `README.md`

4. **Activa permisos de Actions** (para el snake)
   Tu repo → Settings (del repo, no de tu cuenta) → Actions → General → Workflow permissions → **Read and write permissions** → Save

5. **Sube el workflow del snake**
   Crea el archivo `.github/workflows/snake.yml` (la ruta con carpetas es literal) y pega el contenido de `snake.yml`. Al hacer commit a `main`, revisa la pestaña Actions — debe ponerse verde en ~1 minuto y crear la rama `output`.
   El bloque del snake en el README ya apunta a esa rama — no lo actives/verifiques hasta que el Action haya corrido al menos una vez, o se verá roto.

6. **Completa los campos pendientes**
   El banner tiene varios valores marcados como `— agrega tu ... —` (Origin, Education, Portfolio, LinkedIn, Facebook). Para editarlos tendría que regenerar el SVG — dime los datos reales y te entrego una versión actualizada.

7. **Badges**
   Reemplaza `TU-USUARIO` en el badge de LinkedIn por tu handle real. El badge de LinkedIn debe quedarse en azul de marca (`#0A66C2`) — es un bug conocido de shields.io, si le cambias el color el logo desaparece.

## Si algo "no cambia"
Casi siempre es caché del CDN, no un bug:
- Abre `https://raw.githubusercontent.com/.../archivo.svg?v=999` (el `?v=` fuerza a saltarse la caché)
- Revisa que estás viendo el tema correcto (dark.svg solo se ve en modo oscuro de GitHub)
- Confirma que el Action corrió después de tu cambio (pestaña Actions, debe estar en verde)

## Nota sobre el tamaño de archivo
`light.svg` pesa ~1.4MB (el modo claro mantiene el fondo de la foto, generando más puntos que el modo oscuro con fondo segmentado, ~860KB). Ambos están dentro de rangos normales para este tipo de banner, pero si te preocupa el peso, puedo reducir la densidad de puntos.
