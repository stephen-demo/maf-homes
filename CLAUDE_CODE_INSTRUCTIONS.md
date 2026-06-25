# MAF Design Projects — Claude Code Handover Instructions

## Overview

You are taking over a website build for **MAF Design Projects**, a Lagos-based architecture, construction, and interior design firm. The website has already been designed and built. Your job is to **swap in real assets, wire up real project pages, and make the site production-ready**.

Do not redesign anything. The visual language, layout, typography, and color palette are all finalised. Work only within the existing design system.

---

## Folder Structure You Will Receive

```
/
├── index.html                        ← Homepage (complete)
├── project-chevron-duplex.html       ← Template for all project pages
├── images/
│   ├── hero/                         ← Hero background image(s)
│   ├── team/                         ← Michael A.F. and Matthew F.A. photos
│   └── projects/
│       ├── [project-folder-name]/    ← One folder per project
│       │   ├── cover.jpg             ← Used as the card thumbnail on homepage
│       │   ├── 01.jpg
│       │   ├── 02.jpg
│       │   ├── 03.jpg
│       │   └── (more images...)
│       └── ...
```

---

## Task 1 — Replace Placeholder Images with Real Images

### Hero image
- In `index.html`, find the `.hero-bg` div.
- Replace the Unsplash URL in the `background:` CSS with the image from `images/hero/`.
- Use a relative path, e.g. `url('images/hero/hero.jpg')`.

### Team photos
- In `index.html`, find the two `.team-card` blocks in the About section.
- Replace the Unsplash `src` URLs with the correct paths from `images/team/`.
- Michael A.F. → first team card.
- Matthew F.A. → second team card.
- Keep all existing CSS classes. Only change the `src` attribute.

---

## Task 2 — Build a Project Page for Every Project Folder

For every folder inside `images/projects/`, you must:

### 2a. Create a new HTML file
- Duplicate `project-chevron-duplex.html`.
- Name the new file using the project folder name, lowercased, with spaces replaced by hyphens.
  - Example: a folder named `4 Bedroom Duplex Chevron` → `project-4-bedroom-duplex-chevron.html`

### 2b. Update the page content
Fill in the following from the folder name and image contents:

| Field | What to put |
|---|---|
| `<title>` tag | Project name + " — MAF Design Projects" |
| `.project-hero-title` | Project name (split across two lines if long — use `<em>` on the second part) |
| `.project-breadcrumb` | Extract type and location from the folder name if possible |
| Hero background image | First image from the project folder (`01.jpg` or `cover.jpg` if present) |
| `#galleryMainImg` src | Same as hero — first/cover image, full size |
| Gallery thumbnails | All images in the folder, one `.gallery-thumb` per image |
| Meta fields | Location, type, service — infer from folder name; mark as "Architecture & Design" by default if unclear |
| Project specs table | Fill with what can be inferred; leave fields as "—" if unknown |
| Description text | Write a short, professional 2–3 paragraph description in the style already used in `project-chevron-duplex.html`. Match the tone: confident, editorial, warm. Do not use generic filler. Reference the location, the building type, and one specific design quality visible in the images. |
| Related projects | Link to 3 other project pages. Pick ones with different types if possible (e.g. one architecture, one interior, one construction). |

### 2c. Image paths in gallery thumbs
All image `src` attributes must use relative paths like:
```
images/projects/[folder-name]/01.jpg
```

### 2d. `data-img` attribute on thumbnails
Each `.gallery-thumb` needs a `data-img` attribute pointing to the **full-size** version of the image:
```html
<div class="gallery-thumb active" data-img="images/projects/[folder-name]/01.jpg">
  <img src="images/projects/[folder-name]/01.jpg" alt="View 1">
</div>
```

---

## Task 3 — Update the Homepage Project Grid

In `index.html`, find the `#projectsGrid` section. It currently contains 9 placeholder `.project-card` links.

For each real project folder in `images/projects/`:

- Either update an existing card or add a new one.
- Set `href` to the correct project HTML file you created in Task 2.
- Set the `<img src>` to `images/projects/[folder-name]/cover.jpg` (or `01.jpg` if no cover exists).
- Set `data-cat` correctly: `"architecture"`, `"interior"`, or `"construction"` — infer from folder name or image content.
- Update the `.project-card-tag`, `.project-card-name`, and `.project-card-loc` text.

If there are more project folders than the 9 current cards, add more cards using the same HTML structure as the existing ones.

---

## Task 4 — Wire Up the Accordion Form (Optional Enhancement)

The form at the bottom of `index.html` currently logs to the console. If you have access to a form backend (e.g. Formspree, Netlify Forms, or EmailJS), wire it up:

- **Formspree**: Add `action="https://formspree.io/f/YOUR_ID"` and `method="POST"` to a `<form>` wrapper around the form fields.
- **Netlify Forms**: Add `netlify` attribute to the form tag and `name="project-brief"`.
- **EmailJS**: Replace the submit handler in the `<script>` block with an EmailJS `send()` call.

If no backend is available, leave the form as-is. It already shows a success message on submit.

---

## Task 5 — Final QA Checklist

Before finishing, verify:

- [ ] All Unsplash placeholder URLs have been replaced with local image paths
- [ ] Every project folder has a corresponding HTML file
- [ ] Every HTML file is linked correctly from the homepage grid
- [ ] The gallery thumbnails on each project page all work (click to swap main image)
- [ ] The accordion form opens and closes correctly on the homepage
- [ ] The FAQ accordion works (click to expand/collapse)
- [ ] The project filter buttons (All / Architecture / Interiors / Construction) correctly show/hide cards
- [ ] "Work With Us", "Start Your Project", and footer "Start a Project" all scroll to and open the accordion
- [ ] Nav links scroll to the correct sections
- [ ] `rel="noopener"` is present on all external links
- [ ] All `alt` attributes on images are descriptive

---

## Design Rules — Do Not Change These

These are locked. Do not modify them under any circumstances:

- **Fonts**: Cormorant Garamond (headings), Barlow Condensed (labels/nav), Barlow (body)
- **Colors**: `--navy-deep: #111b28`, `--gold: #c8913a`, `--off-white: #f7f4ef`
- **Layout**: Column grid, masonry project grid, sticky sidebar on project pages
- **Section order** on homepage: Hero → Services → Projects → Process → Testimonials → About → FAQ → Accordion Form → Footer
- **CSS class names**: Do not rename or restructure any existing classes

---

## Naming Conventions

| Thing | Convention |
|---|---|
| Project HTML files | `project-[folder-name-hyphenated].html` |
| Image paths | Always relative, never absolute |
| Project folder names | Use exactly as given — just hyphenate for filenames |

---

## Tone Guide for Written Content

When writing project descriptions, follow this style:

- **Voice**: Confident, editorial, warm. Like a high-end architecture studio presenting its work.
- **Structure**: Open with an italic pull-quote sentence. Follow with 2–3 paragraphs of plain prose.
- **What to mention**: The location, the building type, one or two specific design decisions, and how the space serves the client's life.
- **What to avoid**: Generic phrases like "a stunning design" or "beautiful home". Be specific.
- **Length**: 150–250 words per project description.

---

## Contact Details (Use These Everywhere)

```
Phone:   +234 904 110 4480
Email:   m.a.fdesignprojects@gmail.com
Website: https://mafdesignprojects.taplink.ws
WhatsApp: https://wa.me/2349041104480
```

---

## Questions or Ambiguities

If a project folder name is ambiguous (e.g. you can't tell if it's architecture or interior), default to **architecture**.

If a folder contains only one image, use it as both the hero and the single gallery thumbnail. Do not create empty thumbnail slots.

If the folder name contains a location (e.g. "Chevron", "Lekki", "Osun", "Epe", "Ikorodu", "Ajah"), extract it and use it as the location meta field.

---

*Instructions prepared for Claude Code handover. Last updated: 2025.*
