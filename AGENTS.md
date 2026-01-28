# AGENTS.md — Project Creation & Setup Notes

This document records the full, end-to-end creation of the Astro portfolio,
including environment details, project structure, design decisions, and the
terminal troubleshooting required to get `npm` working inside VS Code's Git Bash.

## 1) Goal & Scope
Build a simple, static personal portfolio with three pages (Home, About,
Projects) using Astro + Markdown for content. The site should:
- Educate visitors about Pete McPherson and prior work.
- Capture email signups for a weekly newsletter.

Non-goals:
- No blog/CMS, no auth, no client-side JS beyond HTML forms.
- No animations beyond basic hover/focus states.

## 2) Tech Stack
- Framework: Astro (static-first)
- Content: Markdown files for all page copy
- Styling: Plain CSS
- JS: none required
- Target deployment: Cloudflare Pages

## 3) Template Initialization
Project bootstrapped with the Astro minimal template:
```
npx create-astro@latest . --template minimal --yes --no-install
```

Notes:
- `--no-install` was used to avoid dependency install prompts in the
initial scaffolding step.
- Git was initialized by the Astro CLI.

## 4) Project Structure
Added a clean separation of layouts, components, content, pages, and styles:
```
src/
  components/
    NewsletterForm.astro
  content/
    site.md
    pages/
      home.md
      about.md
      projects.md
  layouts/
    BaseLayout.astro
  pages/
    index.astro
    about.astro
    projects.astro
  styles/
    global.css
```

## 5) Content Architecture (Markdown-first)
All copy lives in Markdown. Page templates only pull in content and render it.

- `src/content/pages/home.md`
  - hero line, intro, project preview data, newsletter copy
- `src/content/pages/about.md`
  - narrative placeholder bio + newsletter copy
- `src/content/pages/projects.md`
  - project list data + newsletter copy
- `src/content/site.md`
  - site title, logo text, nav items, footer text

## 6) Layout & Components

### Base layout
`src/layouts/BaseLayout.astro` provides:
- global font imports (Switzer + Khand via Fontshare)
- header with nav
- footer text pulled from `site.md`

### Newsletter form
`src/components/NewsletterForm.astro`:
- email input + submit button
- accessible label (sr-only)
- placeholder text controlled via Markdown frontmatter

## 7) Styling
`src/styles/global.css` implements:
- clean minimal layout
- white/black palette + single violent red accent
- strong typographic hierarchy (Khand headings, Switzer body)
- responsive layout and spacing
- basic hover/focus states

## 8) Pages Implemented
Each page reads frontmatter and content from its Markdown file:

- `src/pages/index.astro`
  - hero + newsletter + project preview + body content
- `src/pages/about.astro`
  - hero + bio content + newsletter
- `src/pages/projects.astro`
  - hero + project cards + body content + newsletter

## 9) Git Commit
Initial implementation committed:
```
Add Astro portfolio pages with markdown content
```

## 10) npm/Node Setup Troubleshooting (VS Code Git Bash)

### Environment
- OS: Windows
- Terminal: Git Bash (MINGW64) inside VS Code
- Node installed at: `C:\Program Files\nodejs`

### Problems encountered
- `npm: command not found` in Git Bash
- `npm install` failed because `node` was not on PATH for child `cmd.exe`
- Occasional OneDrive `EPERM` cleanup errors

### Working commands (Git Bash)
Check Node:
```
"/c/Program Files/nodejs/node.exe" -v
```

Check npm:
```
/c/Program\ Files/nodejs/npm.cmd -v
```

Install dependencies:
```
export PATH="$PATH:/c/Program Files/nodejs"
/c/Program\ Files/nodejs/npm.cmd install
```

Run dev server:
```
/c/Program\ Files/nodejs/npm.cmd run dev
```

### PowerShell alternative
```
$env:Path = "C:\Program Files\nodejs;" + $env:Path
npm install
npm run dev
```

### OneDrive note
If you see `EPERM` errors in OneDrive paths, retry install or move the project
to a non-synced folder (e.g. `C:\dev\project-name`).

## 11) Future Improvements (Optional)
- Add `package.json` scripts or a `.cmd` helper for Git Bash convenience
- Replace placeholder copy with real content
- Add favicon/branding updates
