---
name: copy-writer
description: Write website page copy based on a sitemap, client brief, and content profile. Produces one markdown file per page. Trigger on "write the copy", "create page content", "write website text". Do not use for research or sitemap creation.
---

1. Read `{project_dir}/client-brief.md`, `{project_dir}/content/research.md` (especially Content Profile section), and `{project_dir}/content/sitemap.md`.
2. For each page in the sitemap, write a file to `{project_dir}/content/copy/{slug}.md`.
3. Each file contains: page title (H1), meta description (under 160 chars), all section headings and body copy, specific CTA text, `[IMAGE: description]` placeholders, `[TESTIMONIAL: source]` placeholders.
4. Follow the content profile strictly:
   - Visual-first: headlines under 8 words, 1-3 sentences per section max, more image placeholders than text, direct CTAs ("Get a Free Estimate" not "Contact Us to Learn More")
   - Information-first: detailed sections allowed, FAQ format where appropriate
5. Match brand tone from the brief. Write for the target customer. No filler phrases ("Welcome to our website", "We are a leading provider").
6. Write `{project_dir}/content/summary.md`: pages planned, messaging themes, top 3 competitor insights, notes for style director (including content profile recommendation for layout density).
7. Write `{project_dir}/content/status.json`: agent, state, deliverables, timestamp.
8. Announce completion.
