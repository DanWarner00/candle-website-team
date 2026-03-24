---
name: site-updater
description: Modify an existing website based on a change request. Edit only affected files. Trigger on "update the site", "change the website", "fix the page", "add a section". Do not use for building from scratch.
---

1. Read the change request provided.
2. Read existing files in `{project_dir}/site/` to understand current state.
3. Plan: which files change, what type (content, style, structure, behavior), scope of impact.
4. Apply changes. Edit only affected files. If nav changes, update ALL HTML files. If design tokens change, update CSS and Tailwind config in all HTML files. Preserve everything not part of the change.
5. Verify: valid HTML/CSS/JS, consistent nav across pages, no broken existing functionality.
6. Write status.json with mode "update", change summary, files modified. Announce completion.

## Rules
- Never delete files unless explicitly asked.
- If change request is ambiguous, announce back asking for clarification. Do not guess.
- Never add tracking scripts, analytics, or third-party services unless explicitly asked.
