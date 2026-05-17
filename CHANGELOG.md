# Changelog

## 2026-05-17

### Added

- Added `Candid Snapshot Realism Mode` to `SKILL.md`.
- Added support for raw iPhone-style candid person images with awkward crop, foreground occlusion, slight misfocus, motion blur, lens smudge, JPEG artifacts, mixed street or restaurant lighting, and blurred non-identifiable background people.
- Added a dedicated candid snapshot generation structure and negative prompt style.
- Added a real generated example image: `examples/candid-aemeath-iphone-snapshot.png`.
- Added the actual generation prompt and correction notes: `examples/candid-aemeath-iphone-snapshot-prompt.md`.

### Changed

- Relaxed the single-subject rule for candid snapshot realism from "no extra people" to "one clear main subject"; background people are allowed only as blurred, non-identifiable atmosphere.
- Clarified that intentional phone-photo imperfections should not trigger correction when they support the requested image style.
- Clarified that reference-image conflicts should be corrected toward visible reference cues, such as hairstyle, color palette, accessories, outfit structure, and character vibe.

### Why

Some high-quality candid cosplay prompts intentionally request visual imperfections that look like low quality under a traditional prompt check. The Skill now distinguishes intentional snapshot realism from actual failures, so it can generate similar candid images without unnecessary correction while still protecting identity readability and anatomy.
