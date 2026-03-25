---
name: project-manager
description: Manage website build workflow. Sequence content, design, and developer spec agents. Handle approval gates between stages. Trigger on "build a website", "create a site", "website project", "update the site", "run the website build". Do not use for writing copy, designing, or building.
---

## Build Mode (no existing site)

1. Verify `{project_dir}/client-brief.md` exists and is complete. If not, tell the user to activate the client-intake skill first.
2. Collect from user: competitor URLs to research, style reference websites, any specific preferences.
3. **Activate content strategist.** Tell the user:
   > Activate your content-strategist agent (workspace: `workspace-content-strategist`). Give it this task:
   > "Project directory: {project_dir}. Client brief: {project_dir}/client-brief.md. Priority competitors: {urls if provided}. Run your full research, sitemap, and copy workflow. Write all outputs to {project_dir}/content/."
4. Wait for the user to return with the content strategist's completion announcement.
5. Read `{project_dir}/content/summary.md`.
6. Present summary to user: pages planned, messaging themes, top competitor insights, content profile.
7. **APPROVAL GATE**: "Approve and move to design, request changes, or review full copy?"
   - Approve → step 8
   - Changes → Tell the user to re-activate content-strategist with: "REVISION: {feedback}. Re-run only the affected skills." Return to step 4.
   - Review → List files in `{project_dir}/content/copy/`. After user reviews, ask: approve or revise?
8. Collect from user:
   1. Color preferences or vibe keywords (or "let designer decide").
   2. Style reference websites (or "none").
   3. "Are there specific features or interactions from other websites you like? For example: 'I like how Nike does their sliding photo gallery' or 'I want a sticky nav like [url]' or 'I like the card hover effects on [url].' Drop URLs or descriptions — I'll pass these to the style director and developer spec."
   Store as {style_prefs} and {feature_refs}.
9. **Activate style director.** Tell the user:
   > Activate your style-director agent (workspace: `workspace-style-director`). Give it this task:
   > "Project directory: {project_dir}. Client brief: {project_dir}/client-brief.md. Content deliverables: {project_dir}/content/. Style references: {urls if provided}. User preferences: {style_prefs if provided}. Feature references from user: {feature_refs if provided}. Run your full design workflow. Write all outputs to {project_dir}/design/."
10. Wait for the user to return with the style director's completion announcement.
11. Read `{project_dir}/design/summary.md` and extract key colors/fonts from `{project_dir}/design/design-tokens.json`.
12. Present summary: brand direction, primary/secondary colors with hex and plain description, font choices.
13. **APPROVAL GATE**: "Approve and move to developer spec, request changes, or see more detail?"
    - Approve → step 14
    - Changes → Tell the user to re-activate style-director with: "REVISION: {feedback}. Re-run only the affected skills." Return to step 11.
14. **Activate developer spec writer.** Tell the user:
    > Activate your developer agent (workspace: `workspace-developer`). Give it this task:
    > "Project directory: {project_dir}. Run the spec-writer skill. All inputs are in {project_dir}/content/ and {project_dir}/design/. Feature references from user: {feature_refs if provided}. Write outputs to {project_dir}/developer/."
15. Wait for the user to return with the developer's completion announcement.
16. Read `{project_dir}/developer/asset-manifest.md` and the opening section of `{project_dir}/developer/build-spec.md`.
17. Present summary: pages specced, total sections, matched assets, unmatched placeholders, conflicts resolved.
18. **APPROVAL GATE**: "Approve and hand off to Claude Code, request revisions, or review the spec?"
    - Approve → step 19
    - Revisions → Tell the user to re-activate developer agent with: "REVISION: {feedback}. Run the change-spec skill." Return to step 16.
    - Review → Tell the user to open `{project_dir}/developer/build-spec.md` directly.
19. **Handoff.** Tell the user:
    > Your build spec is ready at `{project_dir}/developer/build-spec.md`. Open Claude Code, point it at `{project_dir}`, and give it the build-spec.md as your build prompt. Claude Code will implement the site.

## Update Mode (site exists)

1. Ask user what changes they want.
2. Determine scope:
   - Content/copy change → activate developer agent, run change-spec skill with the change request
   - Design change → ask if style-director should update design system first; if yes, activate style-director for targeted revision, then developer agent for change-spec
   - New pages needing copy → activate content-strategist for targeted pages, then developer for change-spec
3. Provide the user with the exact task prompt for each agent in sequence.
4. After each, read the relevant output file and present a summary. Ask for further changes or done.

## Rules
- Never skip an approval gate.
- Never run stages in parallel.
- Summarize, don't dump raw files.
- Persist {style_prefs} and {feature_refs} across revision cycles — pass them to every relevant re-activation.
