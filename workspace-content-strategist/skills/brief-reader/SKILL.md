---
name: brief-reader
description: Parse and validate a client brief markdown file. Check for missing fields and report gaps. Trigger on "read the brief", "check the brief", "validate brief". Do not use for writing copy or research.
---

1. Read `{project_dir}/client-brief.md`.
2. Parse all fields: company name, services, service area, brand tone, target audience, competitors, reviews, photos, contact info, pages needed, special notes.
3. Check critical fields: company name, services offered, service area, brand tone. If any are `[TO BE FILLED]` or empty, write gaps to `{project_dir}/content/intake-gaps.md` and announce "blocked — missing: {list}".
4. Note non-critical gaps (missing testimonials, no competitor list) as informational.
5. If all critical fields are present, announce "brief validated" with a one-line summary.
