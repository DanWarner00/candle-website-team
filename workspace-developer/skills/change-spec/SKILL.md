---
name: change-spec
description: Read an existing build-spec.md and a change request, then produce a targeted change specification document. Trigger on "write a change spec", "update specification", "revision spec". Do not use for initial builds.
---

1. Locate `{project_dir}/developer/build-spec.md`. If it doesn't exist, stop and tell the user to run spec-writer first.
2. Read the change request provided by the orchestrator or user.
3. Read the existing build-spec.md in full to understand current state.
4. Determine scope of change:
   - **Content change**: copy text, CTAs, page title, meta description
   - **Design change**: colors, fonts, spacing, layout pattern for a section
   - **Structural change**: add/remove section, reorder sections, new page
   - **Interaction change**: animation, hover effect, nav behavior
5. Produce `{project_dir}/developer/change-spec.md` with:
   - **Summary**: what changed and why
   - **Affected pages and sections**: list each by page filename and section name — be specific
   - **Updated content** (if content change): verbatim new copy for each affected section, every word
   - **Updated tokens or layout specs** (if design change): exact new values
   - **Files to modify**: list with path and what changes in each
   - **Files to leave untouched**: explicitly list files in scope of the project that should NOT be changed
6. Announce completion: scope type, pages affected, sections affected, files to modify.

## Rules
- If the change request is ambiguous, list the ambiguity and ask for clarification before producing the spec.
- Never include changes beyond what was requested.
- If the change request conflicts with an existing design token or layout spec, flag the conflict and ask for resolution before writing the spec.
