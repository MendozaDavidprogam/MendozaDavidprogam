# MendozaDavidprogam

Personal GitHub profile repository for David Mendoza — Full-Stack Developer from Barquisimeto, Venezuela.

## Project Type

GitHub profile README with lightweight, pure-SVG assets, contribution visualizations, and a terminal-inspired UI.

## Structure

```
.
├── assets/
│   ├── dark.svg            # Banner (dark mode), pure SVG, ~6.4KB
│   ├── light.svg           # Banner (light mode), pure SVG, ~6.4KB
│   ├── stack.svg           # Tech stack badges, pure SVG, ~5.1KB
│   └── quests.svg          # Featured projects panel, pure SVG, ~3.4KB
├── .github/workflows/
│   └── snake.yml            # GitHub Actions workflow for contribution snake animation
├── README.md                 # Profile page with stats, badges, and visualizations
└── CHECKLIST.md              # Deployment and configuration guide
```

## Key Features

### Personal Information
- **Location:** Barquisimeto, Venezuela
- **Role:** Full-Stack Developer
- **Education:** Analista de Sistemas (En Progreso)
- **Portfolio:** https://portafolio-indol-eight.vercel.app

### Banner (assets/light.svg, assets/dark.svg)
- Pure SVG (rect/text/line only) — no `<foreignObject>`, no external HTML/CSS — renders reliably as an `<img>` on GitHub.
- Auto-switches based on GitHub's color scheme preference via `<picture>`.
- All fields are filled in (no placeholder text). LinkedIn and Facebook rows were intentionally removed, not left blank.

### Tech Stack (assets/stack.svg) & Featured Projects (assets/quests.svg)
- Rebuilt from scratch as pure SVG. The previous versions used `<foreignObject>` with CSS flexbox/grid, which most browsers do **not** render when an SVG is loaded via `<img src="...">` (exactly how GitHub displays README images) — that was the root cause of them appearing blank.
- `quests.svg` now lists the 5 real public repositories (app-Clima, pokedex, PortalNoticia-app, TK_CRUD, LABORATORIO-React-NextJS) instead of a fictional quest log.

### GitHub Stats Integration
- Streak stats via `streak-stats.demolab.com`
- GitHub stats + top languages via the public `github-readme-stats.vercel.app` service
- Contribution snake animation (generated via GitHub Actions, published to the `output` branch)

### Design System
- **Primary Color:** `#C8001A` (crimson red)
- **Accent Color:** `#00FF9D` (mint green)
- **Background:** `#06080A` (near-black, terminal aesthetic)
- **Text Primary:** `#E8F0F4`
- **Text Secondary:** `#5A7080`

## Deployment

This is a **GitHub profile repository** — it must be named exactly `MendozaDavidprogam/MendozaDavidprogam` to display on the profile page.

### Required Actions Permissions

For the snake animation to work:
1. Go to Repository Settings → Actions → General
2. Set "Workflow permissions" to "Read and write permissions"
3. Save changes
4. Manually trigger the workflow: Actions → Generate Snake Animation → Run workflow

## Notes

- Banner files were rebuilt from ~1.4MB/864KB (a per-dot "dithering" animation with ~2,850 `<animate>` elements) down to ~6.4KB each — same visual concept, no fabricated content, drastically lighter.
- CDN caching may delay visible changes on GitHub; force refresh with a `?v=` query parameter on the raw URL.
- Snake animation only appears after the first successful Actions run on the `output` branch.
