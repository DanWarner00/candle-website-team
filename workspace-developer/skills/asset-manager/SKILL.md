---
name: asset-manager
description: Manage website image assets. Copy photos from brand-assets to site folder, create styled placeholders for missing images, swap placeholders for real photos. Trigger on "manage images", "add photos", "swap placeholders", "update images". Do not use for code changes or design decisions.
---

1. Read `{project_dir}/site/build-notes.md` to see which placeholders remain.
2. Check `{project_dir}/brand-assets/photos/` for available images.
3. For each placeholder in the HTML files, check if a matching image now exists in brand-assets.
4. If match found: copy image to `site/assets/images/`, replace the placeholder div with a proper `<img>` tag with descriptive alt text.
5. If no match: leave placeholder. Report which placeholders are still unfulfilled.
6. Update build-notes.md with current placeholder count. Announce completion.
