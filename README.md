# Pete McPherson Portfolio (Astro)

Minimal, static portfolio site built with Astro and Markdown. The site focuses
on two goals only: communicating who Pete McPherson is and collecting weekly
newsletter emails.

## Project Overview
- Framework: Astro (static-first)
- Content: Markdown for all page copy
- Styling: Plain CSS
- Pages: Home, About, Projects

## Local Development

### Git Bash (VS Code)
If `npm` is not on PATH, use the full npm path:
```
/c/Program\ Files/nodejs/npm.cmd install
/c/Program\ Files/nodejs/npm.cmd run dev
```

### PowerShell
```
$env:Path = "C:\Program Files\nodejs;" + $env:Path
npm install
npm run dev
```

### Standard commands
```
npm run dev
npm run build
npm run preview
```

## Content Editing
All copy lives in Markdown:
```
src/content/pages/home.md
src/content/pages/about.md
src/content/pages/projects.md
src/content/site.md
```

## Cloudflare Pages Deployment
1) Create a new Cloudflare Pages project and connect this GitHub repo.
2) Set the build configuration:
   - Build command: `npm run build`
   - Build output directory: `dist`
   - Node version: 18+ recommended
3) Deploy.

Astro builds a static site by default, so no adapter is required.
