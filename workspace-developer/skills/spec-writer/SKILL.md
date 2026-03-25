---
name: spec-writer
description: Synthesize all content and design deliverables into a comprehensive developer PRD. Trigger on "write the developer spec", "create build document", "compile the PRD", "developer specification". Do not use for updating existing sites or managing assets.
---

## 1. Input Validation

Check that ALL of the following exist. If anything is missing, list what's absent and stop — do not proceed with partial inputs:
- `{project_dir}/client-brief.md`
- `{project_dir}/content/research.md`
- `{project_dir}/content/sitemap.md`
- At least one file in `{project_dir}/content/copy/`
- `{project_dir}/design/brand-direction.md`
- `{project_dir}/design/design-tokens.json`
- `{project_dir}/design/layout-specs.md`
- `{project_dir}/design/summary.md`

Read ALL of the above, plus list all files in `{project_dir}/brand-assets/`.

## 2. Asset Manifest

Extract every `[IMAGE: description]` placeholder from all copy files. List every file in `{project_dir}/brand-assets/`. Produce three lists:
- **Matched**: placeholder → asset filename (best reasonable match by description)
- **Unmatched placeholders**: no matching asset → will need a styled placeholder div
- **Unused assets**: file exists but no copy placeholder references it

Write to `{project_dir}/developer/asset-manifest.md`.

## 3. Conflict Check

Before writing the spec, identify and resolve any conflicts:
- Page in sitemap that has no copy file → flag as blocker, stop
- Section count in copy vs layout spec mismatch → use copy as source of truth for sections, layout spec as source of truth for visual pattern
- Image placeholder in copy that layout spec doesn't account for → add to unmatched list
- Font, color, or token in layout spec that doesn't exist in design-tokens.json → flag it

## 4. Page Specifications

For each page in the sitemap, write a complete page spec:
- **Page meta**: filename (e.g. `index.html`), URL slug, H1 title, meta description, primary SEO keyword, OG title and description
- **Navigation active state**: which nav item is active on this page
- **Sections in order** — for each section:
  - Section name and purpose
  - Layout pattern from layout-specs.md: grid, split, full-width, cards, hero, etc.
  - Background color token from design-tokens.json
  - **Full verbatim copy** — paste exact text from the copy file, every word
  - Image: matched asset filename, or placeholder div spec (dimensions, background token, label text)
  - CTA: exact button/link text, destination (mailto:, tel:, page slug, or external URL)
  - Animation/interaction from layout-specs.md: scroll trigger, hover effect, entrance animation
  - Mobile notes: how this section adapts at mobile breakpoint

## 5. Global Specification

Write a global spec section covering:
- **Tech stack**: HTML5, Tailwind CSS CDN (specify exact CDN URL with version from design summary), vanilla JS, Google Fonts
- **Google Fonts**: exact @import URL from design summary
- **CSS custom properties**: full dump of all values from design-tokens.json as `:root { --token: value; }` — copy every token
- **Tailwind inline config**: exact `tailwind.config` object extending with token colors and fonts
- **Navigation**: structure, all links with destinations, mobile hamburger behavior (aria attributes, keyboard close on Escape, close on outside click), sticky behavior, active state implementation
- **Footer**: structure, all content verbatim, links, background token
- **Button styles**: primary and secondary — classes, hover state, focus state, active state
- **Responsive breakpoints**: from design tokens — each breakpoint name and px value
- **Scroll animations**: Intersection Observer setup, threshold values, CSS class names, `prefers-reduced-motion` fallback
- **Hover effects**: per component, exact CSS transitions
- **Accessibility**: WCAG AA contrast pairs to verify, heading hierarchy rules, alt text approach per image type, aria attributes for nav and interactive elements, keyboard navigation, focus ring styles

## 6. Implementation Notes

Write an implementation notes section:
- Conflicts found and how they were resolved
- Placeholder div spec: exact HTML/CSS for styled placeholder divs when no image is available
- Contact approach: mailto: and tel: link formats from brief contact info
- Feature references from user (if provided): describe each interaction and how to implement in vanilla JS/CSS
- External libraries needed (name + CDN URL), or "none — CSS and vanilla JS only"
- File structure: every file to create with its full path

## 7. Output

Write everything from sections 4–6 to `{project_dir}/developer/build-spec.md`. This is the master document — it must be complete enough to paste directly into Claude Code as a build prompt.

Announce completion:
- Pages: {count}
- Total sections: {count}
- Matched assets: {count}
- Unmatched placeholders: {count}
- Conflicts found and resolved: {list or "none"}
