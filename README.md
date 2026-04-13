# Akash Verma — Portfolio

A fully data-driven personal portfolio built with **Astro**, **React**, and **Tailwind CSS**. All personal content lives in `src/data/` — no `.astro` or `.tsx` files need to be touched for content updates.

---

## 🚀 Quick Start

```sh
npm install
npm run dev        # Dev server at localhost:4321
npm run build      # Build to ./dist/
npm run preview    # Preview production build locally
```

---

## 📁 Project Structure

```text
/
├── public/
│   ├── images/
│   │   └── education/          # Education institution logos (aktu.jpg, cdac.jpg, ucm.png)
│   └── resumes/
│       └── resume.pdf          # ← Replace this file to update the resume (see below)
│
├── src/
│   ├── components/
│   │   ├── ContactModal.tsx
│   │   ├── MobileNav.tsx
│   │   ├── SkillsArchitecture.tsx   # Interactive SVG radial diagram (not templatized — see note)
│   │   ├── Terminal.jsx
│   │   └── ThemeToggle.tsx
│   │
│   ├── data/                    # ← All content lives here
│   │   ├── home/
│   │   │   ├── profile.json     # Name, bio, social links, stats, CTA, resume path
│   │   │   └── _template.json   # Schema reference
│   │   ├── experiences/
│   │   │   ├── touchnet.json
│   │   │   ├── quotient.json
│   │   │   ├── zycus.json
│   │   │   ├── justdial.json
│   │   │   └── _template.json   # Schema reference
│   │   ├── projects/
│   │   │   ├── *.json           # 20 project files
│   │   │   └── _template.json   # Schema reference (all 5 block types documented)
│   │   ├── education/
│   │   │   ├── ucm.json
│   │   │   ├── cdac.json
│   │   │   ├── aktu.json
│   │   │   └── _template.json   # Schema reference
│   │   └── certifications/
│   │       ├── certifications.json
│   │       └── _template.json   # Schema reference
│   │
│   ├── layouts/
│   │   └── Layout.astro         # Header, footer, nav — reads from profile.json
│   │
│   └── pages/
│       ├── index.astro
│       ├── experience.astro
│       ├── education.astro
│       ├── certifications.astro
│       ├── projects.astro
│       └── skills.astro
```

---

## ✏️ Content Updates

### Personal Info, Social Links, Stats
Edit **`src/data/home/profile.json`**. This single file controls:

| Field | Controls |
|---|---|
| `name` | All page `<title>` tags, terminal greeting |
| `tagline` | Homepage page title suffix |
| `metaDescription` | `<meta description>` on every page |
| `headerHandle` | Header brand link `~/your-handle` |
| `footerName` | Footer copyright name |
| `email` | Contact mailto link |
| `resumeUrl` | Path to resume PDF (default: `/resumes/resume.pdf`) |
| `social[]` | Header icons — GitHub, LinkedIn, Instagram (desktop + mobile) |
| `stats[]` | 6 quick-stat cards on homepage (value, label, GIF, caption) |
| `bio` | Hero paragraph |
| `titleRoulette[]` | Click-to-cycle role titles |
| `cta` | "Ready to Scale?" section heading, body, button label |

### Adding a Social Link
Add an entry to the `social` array in `profile.json`:
```json
{
  "platform": "twitter",
  "label": "Twitter",
  "url": "https://twitter.com/yourhandle",
  "color": "text-[#1DA1F2]"
}
```
Then add the SVG path to the `socialIcons` map in `src/layouts/Layout.astro`.

---

## 📄 Resume

**To update your resume:** replace `public/resumes/resume.pdf` with your new PDF — keep the filename exactly as `resume.pdf`. The download buttons in the header (all pages) and homepage hero will automatically serve the new file. No code changes needed.

---

## 💼 Experiences

Drop a new `.json` file into `src/data/experiences/`. It is automatically picked up and sorted by most-recent start date. See `_template.json` for the full schema.

---

## 🗂️ Projects

Drop a new `.json` file into `src/data/projects/`. It is auto-loaded and sorted (featured first, then by company, then by year). See `_template.json` for all 5 content block types available in the detail panel:

| Block type | Purpose |
|---|---|
| `text` | Paragraph |
| `image` | Figure with optional caption |
| `code` | Syntax-highlighted code block with copy button |
| `callout` | Highlighted box — variants: `info`, `warning`, `success`, `tip` |
| `links` | Badge row with icons — `github`, `doc`, `blog`, `link` |

Files prefixed with `_` (e.g. `_template.json`) are excluded from all glob imports and will never appear on the page.

---

## 🎓 Education

Drop a new `.json` file into `src/data/education/`. Auto-loaded and sorted by most-recent start date. See `_template.json` for the schema and image path convention (`/images/education/filename.ext`).

---

## 🏅 Certifications

Edit `src/data/certifications/certifications.json` directly (it's a single array file). See `_template.json` for field details including available `color` options per provider.

---

## 🛠️ Skills Page

The **Skills Architecture** page (`/skills`) renders an interactive SVG radial diagram built entirely inside `src/components/SkillsArchitecture.tsx`.

**Why it is not templatized:** The skill data (names, icons, positions) is deeply interwoven with SVG geometry calculations (radii, ellipse coordinates, rotation angles). Extracting data to JSON would require refactoring the entire layout math, with a high risk of breaking the visual. To update skills on this page, edit `SkillsArchitecture.tsx` directly.

---

## 🚢 Deployment (GitHub Pages)

Everything lives in a single public repo: **`akash-cloudtech/portfolio`**

| Branch | Purpose |
|---|---|
| `main` | Astro source code |
| `gh-pages` | Built `dist/` output — served by GitHub Pages |

### Deploy

```sh
npm run deploy
```

This command builds the site → pushes the compiled `dist/` output to the `gh-pages` branch → GitHub Pages serves it at `https://akash-cloudtech.github.io/portfolio/`.

### Workflow

```sh
# Save source changes
git add . && git commit -m "your message" && git push

# Publish to live site
npm run deploy
```

### First-time GitHub Pages setup
1. Go to `akash-cloudtech/portfolio` on GitHub
2. Settings → Pages
3. Source: **Deploy from a branch** → Branch: `gh-pages` → folder: `/ (root)`
4. Save
