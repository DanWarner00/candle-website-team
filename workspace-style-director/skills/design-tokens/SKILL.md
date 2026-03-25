---
name: design-tokens
description: Produce a structured JSON design system with colors, typography, spacing, borders, shadows, transitions, and breakpoints. Trigger on "create design tokens", "design system", "color palette and fonts". Do not use for layout specs or brand direction.
---

1. Read `{project_dir}/design/brand-direction.md` and `{project_dir}/client-brief.md`.
2. Read the token schema from the `references/` subfolder of this skill: `C:\Users\warnd\.openclaw\workspace-style-director\skills\design-tokens\references\design-tokens-schema.json`. Read it before generating any tokens.
3. Produce `{project_dir}/design/design-tokens.json` matching the exact schema structure.
4. Every value must be a real, usable CSS value. No placeholders.
5. If the brief has existing brand colors or logo, derive palette from those. Otherwise build from brand personality.
6. All text/background combos must meet WCAG AA contrast (4.5:1 normal, 3:1 large).
7. Only Google Fonts or system fonts. Include full @import URL.
8. Announce completion with primary color, secondary color, and font names.
