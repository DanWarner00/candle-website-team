---
name: site-builder
description: Build a full static website from content and design specifications. Creates HTML, CSS, and JS files. Trigger on "build the site", "create the website", "generate the pages". Do not use for updating existing sites.
---

1. Read `{project_dir}/client-brief.md`, `{project_dir}/content/sitemap.md`, all files in `{project_dir}/content/copy/`, `{project_dir}/design/design-tokens.json`, `{project_dir}/design/layout-specs.md`, `{project_dir}/design/summary.md`.
2. Block if design-tokens.json or sitemap.md missing.
3. Create directory structure: `{project_dir}/site/`, `css/`, `js/`, `assets/images/`.
4. Copy photos from `{project_dir}/brand-assets/photos/` to `site/assets/images/`. Copy logo if present.
5. Create `css/custom.css`: all design tokens as CSS custom properties on `:root`, base resets, custom animations, responsive overrides, `prefers-reduced-motion` block.
6. For each page: create HTML file with DOCTYPE, meta tags (charset, viewport, description, OG tags), Google Fonts link, Tailwind CDN + inline config with token colors/fonts, link to custom.css, consistent header/nav with mobile hamburger and active state, main content section-by-section per layout-specs using verbatim copy, consistent footer, script tag for main.js. Use brand-asset images where matching, styled placeholder divs where not. `mailto:` for contact CTA, `tel:` for phone.
7. Create `js/main.js`: mobile nav toggle (with aria attributes, keyboard nav, close on escape/outside click), Intersection Observer scroll animations respecting `prefers-reduced-motion`, active nav state, smooth scroll for anchors, gallery lightbox if applicable. Vanilla JS only. If user feature references were provided, implement the specified interaction patterns (sliding galleries, specific nav behaviors, hover effects, etc.) using vanilla JS and CSS. Match the referenced behavior as closely as possible while keeping it consistent with the design tokens and layout specs. If a referenced interaction requires a lightweight external library, note it in build-notes.md with the CDN link used.
8. Quality checks: all pages exist, all links work, all copy from content files is present, design tokens applied, responsive classes used, accessibility basics (alt tags, heading hierarchy, labels, contrast).
9. Write `{project_dir}/site/build-notes.md`: pages built, unfulfilled placeholders, deviations, preview instructions ("open index.html in browser").
10. Write status.json. Announce completion.
