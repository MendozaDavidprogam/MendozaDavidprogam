# 📋 Checklist — Actualización con retrato tamizado (dithering)

## ✅ Qué se hizo en esta ronda

### 1. Banner con tu foto real (`assets/dark.svg`, `assets/light.svg`)
- Se procesó tu foto con un pipeline real en Python (Pillow + NumPy + SciPy):
  segmentación del fondo por distancia de color + saturación → recorte cabeza/hombros →
  autocontraste → unsharp mask → contraste 1.3x → **dithering Floyd–Steinberg**.
  - Los puntos se dibujan como un único `<path>` (rects `crispEdges`), **sin `foreignObject`**.
  - Panel `SYSTEM.INFO` a la derecha, igual que antes: ciudad, carrera, portafolio correctos,
    **sin LinkedIn ni Facebook**.
  - Peso: **~178KB** por archivo. El diseño original de 17K puntos + 3 logos morphing
    (descrito en el Master Prompt) pesa 900KB–1MB y requiere iteración manual de contraste/recorte
    en varias vueltas — para un README de perfil no vale la pena ese costo. Si más adelante quieres
    esa versión completa con logos animados, se puede montar, pero es un proyecto aparte, no un ajuste.

### 2. `assets/stack.svg` y `assets/quests.svg` — reconstruidos otra vez
- Los archivos que subiste (`stack.svg`, `quests.svg`, `header.svg`) volvían a usar `foreignObject`
  con HTML/CSS interno → **se renderizan en blanco** cuando GitHub los carga como `<img>` (lo comprobé
  renderizando tu `header.svg` tal cual lo subiste: sale una imagen completamente vacía).
- Reconstruidos en SVG puro, igual que la vez anterior, con la misma paleta.

### 3. `assets/stats.svg` — nuevo, sin dependencias externas
- Tu captura de pantalla mostraba "GitHub Stats" y "Top Languages" rotos (ícono de imagen caída):
  es el error **"API rate limit exceeded"** del servicio público `github-readme-stats.vercel.app`,
  descrito también en tu propio PDF de setup.
- En vez de pedirte que montes tu propia instancia en Vercel (Fase 2 del Master Prompt — requiere
  crear un token de GitHub y desplegar en tu cuenta, algo que no puedo hacer por ti desde este chat),
  generé una tarjeta de estadísticas **propia y estática**, con tus datos reales tomados de tu perfil
  público (8 repos, 3 estrellas, 1 seguidor, 9 siguiendo, lenguajes reales de tus repos, tus logros).
  Esta tarjeta nunca se cae porque no depende de ningún servicio de terceros.
- Dejé también la tarjeta de racha (`streak-stats.demolab.com`) porque en tu captura sí funcionaba,
  con una nota aclaratoria por si algún día falla.
- Quité la "Contribution Graph" de `github-readme-activity-graph.vercel.app` (otro servicio público
  con límite de peticiones) porque es redundante con la serpiente de contribuciones, que ya tienes
  funcionando vía GitHub Actions.

### 4. Badges finales
- Quité el badge de GitHub del pie (tu propio PDF lo recomienda: en tu propio perfil es circular/redundante).
- Sin LinkedIn ni Facebook, como pediste.
- Portfolio + Email.

## 🔧 Opcional — para estadísticas 100% dinámicas (no obligatorio)

Si en algún momento quieres que `stats.svg` se actualice solo (en vez de ser un snapshot fijo),
la única forma real es la Fase 2 del Master Prompt: self-host de `github-readme-stats` en tu propio
Vercel con tu token. Son pasos que solo puedes hacer tú (requieren tu cuenta de GitHub y de Vercel):

1. `github.com/settings/tokens` → Tokens (classic) → scope `repo` → sin expiración.
2. Fork de `anuraghazra/github-readme-stats`.
3. Vercel → Import del fork → variable de entorno `PAT_1` = tu token → Deploy.
4. Me pasas la URL de tu instancia y actualizo el README para usarla.

Sin esto, `stats.svg` sigue siendo 100% confiable, solo que hay que regenerarlo a mano cuando
quieras refrescar los números (puedo hacerlo cuando me lo pidas).

## 📤 Cómo publicar

No tengo permiso de escritura sobre tu repo de GitHub, así que sube los archivos tú:

1. Descarga el ZIP adjunto (trae `README.md` + `assets/` completo).
2. En `MendozaDavidprogam/MendozaDavidprogam` → **Add file → Upload files**.
3. Sube los 5 SVG dentro de `assets/` y el `README.md` en la raíz (incluso puedes borrar
   `header.svg` de la raíz si lo habías subido ahí — ya no se usa).
4. Commit a `main`. Espera 1–2 min por el caché de GitHub (o agrega `?v=1` a la URL cruda para forzar).
