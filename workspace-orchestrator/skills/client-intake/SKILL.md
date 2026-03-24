---
name: client-intake
description: Create a new client brief, interview the user for project details, or validate an existing brief. Trigger on "new client", "client brief", "start a project", "project intake". Do not use for design, code, or content writing.
---

1. Ask the user for the project directory path.
2. Check if `{project_dir}/client-brief.md` exists.
3. If it does not exist, read the brief template from `{baseDir}/references/brief-template.md`.
4. Interview the user in conversational blocks to fill the template:
   - Block 1: Company name, owner(s), years in business, location/service area
   - Block 2: Services offered, specialty/flagship service
   - Block 3: Brand tone (offer examples: professional, friendly, rugged, modern, premium), target customer
   - Block 4: Pages needed (suggest default: Home, Services, Gallery, About, Contact), existing reviews/testimonials, photos (location on disk), contact info (phone, email)
   - Block 5: Things to avoid, competitor websites to reference, style reference websites
5. Write the completed brief to `{project_dir}/client-brief.md`.
6. Present a summary: "{company}, serving {area}, {n} pages, tone: {tone}."
7. Wait for user confirmation before considering the brief complete.
8. If the brief already exists, scan for `[TO BE FILLED]` fields. Report gaps and ask the user to fill them.
