---
name: person-image-prompt-gate
description: Validate and refine character, cosplay, portrait, anime standing art, and person-focused image generation prompts before generating images. Use when the user asks Codex to create a person image and wants prompt completeness checks, conflict detection, practical prompt corrections, and generation only after the prompt passes.
---

# Person Image Prompt Gate

Use this skill before generating any person-focused image when the user wants validation-first behavior.

Workflow: inspect the prompt, verify it against the 9-module method, pause on conflicts, propose a corrected prompt, and generate only when the prompt is coherent.

## Operating Rule

Do not generate immediately if the prompt has an internal contradiction, missing critical module, unsafe ambiguity, or a style/shot conflict that will likely degrade the image.

If the prompt passes, generate directly with the image tool. If it fails, explain the issue concisely, provide a revised prompt, and wait for the user to confirm or ask to proceed.

## 9-Module Person Image Method

Check the prompt in this order:

1. **Image type**: portrait, cosplay photo, anime character art, full-body standing art, fashion cover, cinematic poster, etc.
2. **Single-subject constraint**: one person only, no extra people, no collage, no grid.
3. **Subject identity and face**: character/person, age, facial features, hairstyle, expression, gaze, makeup.
4. **Styling system**: outfit, colors, materials, accessories, props, character-specific details.
5. **Scene and world**: location, time, background objects, worldbuilding cues.
6. **Composition and camera**: framing, shot size, angle, aspect ratio, foreground/background, focus.
7. **Action and body language**: pose, movement, hand placement, gaze direction, emotion.
8. **Light and color**: sunlight, flash, neon, rim light, Tyndall rays, color palette, contrast.
9. **Texture and finish**: skin, hair, fabric, water droplets, film grain, anime movie quality, cinematic grading, negative prompts.

## Pass Criteria

A prompt passes when:

- The requested image type is clear.
- It is explicitly single-person if the user wants one person.
- The subject identity is described enough for the style goal.
- Outfit, accessories, and props do not contradict the character or scene.
- Scene and action can happen physically in the same frame.
- Camera angle and pose are compatible.
- Lighting and atmosphere support the scene.
- Negative prompts block likely failures.

## Common Conflicts

Pause and correct these before generation:

- **Camera-action conflict**: "front full-body standing shot" plus "lying down", or "first-person POV" plus an impossible full frontal symmetrical shot.
- **Pose-motion conflict**: "running" plus "sitting still", or "lying on a chair" plus "standing full-body".
- **Scene-style conflict**: "beach swimsuit" plus "exact original costume" without saying it is a summer reinterpretation.
- **Character fidelity conflict**: "faithful to original" while replacing the whole outfit. Preserve hair, color palette, ornaments, temperament, and signature props instead.
- **Composition overload**: asking for full body, close-up face, detailed background, water droplets, distant objects, and first-person angle with no hierarchy.
- **Multi-person risk**: names, reflections, crowd backgrounds, collage/grid language, or plural "characters".
- **Age ambiguity**: if sensual framing, swimwear, or seductive language appears, ensure the subject is an adult. If not adult, pause and ask for an adult age or remove the sexualized framing.

## Correction Pattern

When correcting, structure the answer like this:

1. State: "先暂停，不生图。"
2. List the specific conflict or missing module using concrete wording.
3. Provide a revised prompt organized by the 9 modules.
4. Say that this version now passes the method and can be generated after confirmation.

Keep corrections practical and short. Do not over-explain theory.

## Generation Prompt Structure

When a prompt passes, generate from this structure:

```text
[Image type], single subject, one adult person only.

Subject: [character/person identity], [age], [face], [hair], [expression], [gaze], [temperament].

Styling: [outfit], [colors], [materials], [accessories], [props], [character-specific details]. If this is a swimsuit or alternate outfit, phrase it as an official summer/beach reinterpretation while preserving recognizable character cues.

Scene: [location], [background], [time/weather], [worldbuilding elements].

Camera and composition: [shot size], [angle], [POV], [orientation/aspect], [focus], [background blur].

Action and body language: [pose or motion], [hand placement], [gaze direction], [body line], [emotion].

Lighting and texture: [main light], [rim/highlight], [color palette], [water/particles/fabric/skin/hair texture], [film/anime/cinematic finish].

Negative: no extra people, no collage, no grid, no product, no text, no watermark, no deformed hands, no extra limbs, no low quality, no blurry subject.
```

## Character Adaptation Rule

For existing game/anime characters, avoid claiming perfect canonical accuracy if the outfit is changed. Instead:

- Preserve recognizable color palette, hairstyle, accessories, temperament, and motifs.
- Describe the new outfit as a themed reinterpretation, such as "official summer beach variant".
- Include character-specific ornaments and props where useful.
- Do not add unrelated accessories that fight the character identity.

## Direct Generate Rule

If the user's prompt is coherent and complete, do not ask extra questions. Rewrite internally into a clean generation prompt and call the image generation tool.

After image generation, do not add commentary unless the active image tool policy requires otherwise.
