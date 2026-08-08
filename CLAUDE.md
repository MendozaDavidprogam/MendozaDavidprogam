# MendozaDavidprogam

Personal GitHub profile repository for David Mendoza — Full-Stack Developer from Barquisimeto, Venezuela.

## Project Type

GitHub profile README with animated SVG assets, contribution visualizations, and modern UI/UX design.

## Structure

```
.
├── assets/
│   ├── dark.svg           # Animated banner (dark mode, ~864KB)
│   ├── light.svg          # Animated banner (light mode, ~1.4MB)
│   ├── quests.svg         # Mission log visualization
│   └── stack.svg          # Tech stack inventory
├── .github/workflows/
│   └── snake.yml          # GitHub Actions workflow for contribution snake animation
├── README.md              # Profile page with stats, badges, and visualizations
└── CHECKLIST.md           # Deployment and configuration guide
```

## Key Features

### Personal Information
- **Location:** Barquisimeto, Venezuela
- **Role:** Full-Stack Developer
- **Education:** Systems Analysis (In Progress)
- **Portfolio:** https://portafolio-indol-eight.vercel.app

### Animated Banner
- Dual-theme SVG banners (dark/light) with dithering effect
- Morphing tech logos (React/Node/`</>`)
- Auto-switches based on GitHub's color scheme preference

### GitHub Stats Integration
- Streak stats via `streak-stats.demolab.com`
- GitHub stats using public `github-readme-stats.vercel.app` service (no self-hosting required)
- Top languages visualization in compact layout
- Contribution snake animation (generated via GitHub Actions)
- Table-based layout for side-by-side stats display

### Design System (UI/UX Pro Max Applied)
- **Primary Color:** `#C8001A` (crimson red) — used for titles and primary actions
- **Accent Color:** `#00FF9D` (mint green) — used for highlights and interactive elements
- **Background:** `#0D1117` (GitHub dark) — consistent with GitHub's native dark mode
- - **Text Primary:** `#E6EDF3` (light gray)
- **Text Secondary:** `#7D8590` (muted gray)
- Modern card-based layout with clear visual hierarchy
- Responsive badges with consistent styling
- Professional spacing and alignment

## Deployment

This is a **GitHub profile repository** — it must be named exactly `MendozaDavidprogam/MendozaDavidprogam` to display on the profile page.

### Setup Complete ✅

The profile is ready to use with:
- ✅ Updated personal information (Venezuela - Barquisimeto, Full-Stack Developer)
- ✅ Portfolio link integrated
- ✅ Modern UI/UX design applied
- ✅ GitHub stats using public API (no self-hosting required)
- ✅ Snake animation workflow configured
- ✅ Social links optimized (removed LinkedIn/Facebook as requested)

### Required Actions Permissions

For the snake animation to work:
1. Go to Repository Settings → Actions → General
2. Set "Workflow permissions" to "Read and write permissions"
3. Save changes
4. Manually trigger the workflow: Actions → Generate Snake Animation → Run workflow

The snake SVG will be generated and committed to the `output` branch.

### GitHub Actions

The snake animation workflow:
- Runs every 12 hours (cron schedule)
- Triggers on push to `main`
- Generates light/dark snake SVGs from contribution graph
- Publishes to `output` branch

## Tech Stack Represented

Based on the profile presentation:
- Frontend: React, HTML/CSS
- Backend: Node.js
- Version Control: Git/GitHub
- Deployment: Vercel (for stats hosting)
- CI/CD: GitHub Actions

## Notes

- **LinkedIn and Facebook removed** as requested — profile focuses on GitHub, Portfolio, and Email
- **GitHub stats fixed** — now using public API service instead of self-hosted, solving visibility issues
- **UI/UX Pro Max applied** — modern design with consistent color system, proper spacing, and visual hierarchy
- **Table layout** — stats are displayed side-by-side for better visual balance
- Banner SVG files are large (~864KB dark, ~1.4MB light) due to dithering point density — intentional for visual quality
- CDN caching may delay visible changes; force refresh with `?v=` query parameter
- Snake animation only appears after first successful Actions run
- All widgets use the `radical` theme matching the custom color palette
- Profile designed to attract recruiters and showcase professional skills
- Code block in header provides structured information in developer-friendly format
