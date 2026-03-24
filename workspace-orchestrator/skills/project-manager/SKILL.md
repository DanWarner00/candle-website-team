---
name: project-manager
description: Manage website build workflow. Sequence content, design, and development agents. Handle approval gates between stages. Trigger on "build a website", "create a site", "website project", "update the site", "run the website build". Do not use for writing copy, designing, or coding.
---

## Build Mode (no existing site)

1. Verify `{project_dir}/client-brief.md` exists and is complete. If not, tell the user to run client-intake first.
2. Collect from user: competitor URLs to research, style reference websites, any specific preferences.
3. Spawn content-strategist agent:
   - `sessions_spawn` with `agentId: "content-strategist"`
   - Task: "Project directory: {project_dir}. Client brief: {project_dir}/client-brief.md. Priority competitors: {urls if provided}. Run your full research and copy workflow. Write all outputs to {project_dir}/content/."
4. Wait for completion. Read `{project_dir}/content/summary.md`.
5. Present summary to user: pages planned, messaging themes, top competitor insights, content profile.
6. APPROVAL GATE: "Approve and move to design, request changes, or review full copy?"
   - Approve → step 7
   - Changes → re-spawn content-strategist with "REVISION: {feedback}" appended. Return to step 4.
   - Review → list files in `{project_dir}/content/copy/`, collect feedback, then ask approve or revise.
7. Collect from user:
   1. Color preferences or vibe keywords (or "let designer decide").
   2. Style reference websites (or "none").
   3. "Are there specific features or interactions from other websites you like? For example: 'I like how Nike does their sliding photo gallery' or 'I want a sticky nav like [url]' or 'I like the card hover effects on [url].' Drop URLs or descriptions — I'll pass these to the designer and developer."
   Store as {style_prefs} and {feature_refs}.
8. Spawn style-director agent:
   - `sessions_spawn` with `agentId: "style-director"`
   - Task: "Project directory: {project_dir}. Client brief: {project_dir}/client-brief.md. Content deliverables: {project_dir}/content/. Style references: {urls if provided}. User preferences: {style_prefs if provided}. Feature references from user: {feature_refs if provided}. Run your full design workflow. Write all outputs to {project_dir}/design/."
9. Wait for completion. Read `{project_dir}/design/summary.md` and extract key colors/fonts from `{project_dir}/design/design-tokens.json`.
10. Present summary: brand direction, primary/secondary colors with hex and plain description, font choices.
11. APPROVAL GATE: "Approve and move to development, request changes, or see more detail?"
    - Approve → step 12
    - Changes → re-spawn style-director with "REVISION: {feedback}" appended. Return to step 9.
12. Spawn developer agent:
    - `sessions_spawn` with `agentId: "developer"`
    - Task: "Project directory: {project_dir}. Mode: build. Client brief: {project_dir}/client-brief.md. Content: {project_dir}/content/. Design: {project_dir}/design/. Feature references from user: {feature_refs if provided}. Build the full site to {project_dir}/site/."
13. Wait for completion. Read `{project_dir}/site/build-notes.md`.
14. Present: pages built, placeholders remaining, "Open {project_dir}/site/index.html to preview."
15. "Make changes or done?" → Changes: go to Update Mode. Done: confirm completion.

## Update Mode (site exists)

1. Ask user what changes they want.
2. Determine scope:
   - Content/structural change → spawn developer with mode: update
   - Design change → ask if style-director should update design system first, then developer
   - New pages needing copy → spawn content-strategist for targeted pages, then developer
3. Spawn appropriate agent(s) with change request.
4. Present results. Ask for further changes or done.

## Rules
- Never skip an approval gate.
- Never spawn agents in parallel for build mode.
- Summarize, don't dump raw files.
- Persist user preferences across revision cycles.
