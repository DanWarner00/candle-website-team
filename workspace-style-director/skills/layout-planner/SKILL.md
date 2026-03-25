---
name: layout-planner
description: Create section-by-section layout specifications and animation/interaction direction for every page. Trigger on "plan the layouts", "layout specs", "page layouts and animations". Do not use for design tokens or brand direction.
---

1. Read `{project_dir}/content/sitemap.md`, `{project_dir}/design/design-tokens.json`, `{project_dir}/design/brand-direction.md`, and `{project_dir}/content/summary.md`.
2. If feature/interaction references were provided by the user, research each referenced URL or description. Analyze the specific interaction pattern the user liked (sliding gallery, sticky nav, card hover, parallax section, etc.). Document how to adapt it for this project's brand and content profile. Incorporate these patterns into the layout specs and interactions section. If a reference conflicts with the content profile (e.g., a heavy animation reference for a visual-first site that should stay clean), note the conflict and suggest a lighter version that captures the same feel.
3. For each page in sitemap, write layout spec: layout type, section-by-section breakdown (pattern, alignment, background token, interactive elements, image placement), mobile adaptation notes.
4. Write global components section: navigation (style, sticky behavior, mobile menu), footer (layout, content, background), buttons (primary/secondary styles, states), cards (if used), section transitions.
5. Write animation specs: page load animations, scroll-triggered animations (Intersection Observer, no libraries), hover effects, micro-interactions. All must respect `prefers-reduced-motion`.
6. Write everything to `{project_dir}/design/layout-specs.md`.
7. Write `{project_dir}/design/summary.md`: brand overview, color rationale, font rationale, developer notes, Google Fonts URLs, recommended libraries (or "none — CSS only"), Mobile & Responsive Notes (mobile nav pattern — hamburger or alternative; breakpoint behavior for each major layout type; touch target sizing requirements; any layout changes per breakpoint that differ from desktop).
8. Announce completion.
