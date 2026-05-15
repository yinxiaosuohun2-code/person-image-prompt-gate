# Person Image Prompt Gate

[中文说明](README.md)

Person Image Prompt Gate is a Codex Skill for validating person-focused image generation prompts before generating images. It checks whether a prompt is complete and whether it contains conflicts in camera, pose, styling, age, subject count, or scene logic. If the prompt passes, Codex generates the image directly. If not, Codex pauses and suggests a corrected version first.

## Credits

This Skill was inspired by the open-source project [EvoLinkAI/awesome-gpt-image-2-API-and-Prompts](https://github.com/EvoLinkAI/awesome-gpt-image-2-API-and-Prompts).

Thanks to the original project authors and community contributors for sharing a large collection of GPT-Image-2 API and prompt examples. This Skill is derived from observing, filtering, and analyzing the person-generation cases in that project, then turning those observations into a validation workflow for character, cosplay, portrait, and illustration prompts. This repository does not copy the original project's example images or full prompt content.

For broader GPT-Image-2 API examples, prompt references, and community contributions, please visit the original project.

## Use Cases

- Anime character standing art
- Cosplay character images
- Single-character posters
- Person-focused illustrations
- Realistic or semi-realistic portrait-style images
- Themed variants of game or anime characters

This Skill is not intended for group images, ecommerce images, advertising visuals, product images, pure landscapes, or non-person subjects.

## The 9-Module Prompt Check

The Skill checks person prompts in this order:

1. Image type
2. Single-subject constraint
3. Subject identity and face
4. Styling system
5. Scene and world
6. Composition and camera
7. Action and body language
8. Light and color
9. Texture and final finish

If the prompt contains conflicts such as "full-body front standing shot" plus "lying on a chair", "first-person top-down view" plus "complete full-body front view", or "exact original outfit" plus "swimsuit redesign", Codex should pause and provide a corrected version before generating.

## Installation

Clone this repository into your Codex skills directory:

```powershell
git clone https://github.com/YOUR_NAME/person-image-prompt-gate.git "$env:USERPROFILE\.codex\skills\person-image-prompt-gate"
```

Restart Codex, then call:

```text
$person-image-prompt-gate
```

You can also simply ask Codex to generate a person image and specify that the prompt should be validated first.

## Real Interaction Examples

The following examples come from real interactions during the creation of this Skill. The conversations are shortened for readability. They show the main behavior: validate first, then either pause for correction or generate directly.

### Example 1: Cosplay Image, Camera-Pose Conflict Corrected

The user requested a single-character cosplay image: Cantarella, Maldives beach, European vintage umbrella, deep purple swimsuit, light purple sheer beach skirt, strong sunlight, refractive water droplets, and cinematic quality.

The prompt also contained a conflict: "first-person standing top-down view, full-body medium front shot" plus "the character lies on a white beach chair." The Skill corrected the prompt by keeping the beach chair, diagonal composition, purple styling, and relaxed atmosphere, while removing the incompatible first-person standing top-down camera instruction.

<img src="examples/cosplay-cantarella-beach.png" alt="COS beach character example" width="420">

### Example 2: Anime Character Art, Complete Structure, Direct Generation

The user requested a single anime movie-style character image: Feixue, red-and-white swimsuit, beach and shallow water, full-body medium front shot, half-turn smile, strong sunlight, Tyndall light rays, hair highlights, water droplets, sailboats, and palm trees.

Validation result: image type, single-subject constraint, character identity, styling, scene, camera, action, lighting, and negative prompts were complete and compatible, so the image was generated directly.

<img src="examples/anime-feixue-beach.png" alt="Anime beach character example" width="420">

### Example 3: Character Summer Variant with Recognizable Identity

The user requested Aemeath from Wuthering Waves as a single anime standing-art image: pink swimsuit, shallow sea, small sailboat, racing into sunlight, joyful smile, distant sailboats and palm trees.

Validation focus: a swimsuit redesign should not be described as "perfectly canon." The prompt should frame it as a summer shallow-sea variant while preserving recognizable cues: pink hair, original color palette, electronic ghost-like temperament, dreamy technology feel, and character-specific ornaments. The prompt passed and was generated directly.

<img src="examples/anime-aemeath-sailboat.png" alt="Anime sailboat character example" width="420">

### Example 4: Reference Images, Adult Age, and Dynamic Pose

The user provided character references and requested an anime cinematic dynamic illustration: one adult female character, Aemeath summer shallow-sea variant, 22+ years old, pink swimsuit, surfboard, full-body medium front shot, diagonal composition, clear silhouette, strong sunlight, splashing water droplets, and cinematic anime finish.

Validation result: adult age was explicit, the character-variant logic was coherent, the dynamic action matched the camera framing, background elements were layered, and the negative prompt covered extra people, collage, text, watermark, deformed hands, and low-quality risks. The image was generated directly.

<img src="examples/anime-aemeath-surfboard.png" alt="Anime surfboard character example" width="520">

## Minimal Prompt Template

```text
$person-image-prompt-gate
Image type: [anime standing art / cosplay image / character poster / illustration]
Single subject: one person only, adult character
Subject identity: [character name, age, face, hairstyle, expression, temperament]
Styling system: [outfit, colors, materials, accessories, props, recognizable character cues]
Scene and world: [location, time, background elements, worldbuilding cues]
Composition and camera: [full body / half body / close-up, front / side / top-down, focus, background blur]
Action and body language: [standing, running, turning back, sitting, hand placement, emotion]
Light and color: [sunlight, neon, flash, rim light, palette]
Texture and final finish: [skin, hair, fabric, water droplets, cinematic quality, clarity]
Negative: no extra people, no collage, no grid, no text, no watermark, no deformed hands.
```

## License

Choose an open-source license that matches your publishing needs, such as the MIT License. The original project's content and license should be checked on its own repository page.
