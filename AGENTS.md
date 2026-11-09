# ORMA MOTION — Agent entrypoint

This repository (`ormapro/orma-motion`) holds the **technical engine, source, and production standards** for Orma Motion. It includes Bang Motion v1.19.0 under MIT; preserve attribution and licensing. The upstream `SKILL.md` and starter files are **not** proof that a new commercial workflow or renderer is already implemented.

## Read first for any production or engine task

1. **`docs/ORMA_MOTION_CHARACTER_FIRST_WORKFLOW.md`** — owner-directed production standard (10 Nov 2026), particularly when characters, backgrounds, and animated props are involved.
2. **`SKILL.md`**, **`references/anti-ppt.md`** and relevant reference/starter.
3. **`docs/ORMA_MOTION_DEVELOPMENT_HANDOFF_2026-11-06.md`** for technical limitations and historical stage notes. Date-bound status is a snapshot; inspect source and newer decisions before claiming a feature exists.
4. For currently active ChatGPT projects that still specify Member Area routing, read `omar-mcht/orma-member-area/docs/START_HERE.md` first as those project instructions require. The owner is considering simplifying future coordination directly into this repo; **that migration is not yet verified or complete**.

## Production non-negotiables

- **Start from the entire voiceover/script**, not a short sample: whole-video beat sheet, full Character Asset Sheet, pose–expression–action matrix, sets, props, UI, and reusable asset manifest must be defined **before** asset generation/motion proof.

- **Mandatory output FPS >=30.** Default 30 fps unless the brief specifies more; 60 fps is valid. Never render or deliver a 24/25-fps finished ad. Set animation timeline, frame export, encoding and QA to the same target FPS. Do not merely relabel low-fps frames as 30 fps; verify with `ffprobe` and decoded-frame count. Audio at 24 kHz is unrelated to video 24 fps.
- **Terminology:** always name the character specification **Character Asset Sheet** and the location/prop specification **Set & Prop Inventory**.
- **Character-first, not composite-crop-first:** make each reusable character as a separate sprite/rig system with its required views, emotions, and action poses; create independent backgrounds and props. **Do not cut a character out of a finished storyboard/image and move that one cutout as the entire animation**.
- 2.5D means coherent layered worlds and action with independently controlled character states/objects; parallax or zoom alone is not enough. Use sprite/pose swaps or true joint rigs when necessary. Borrow joint rig techniques from `references/kartun-panggung.md` without inheriting its cartoon art style.
- Use original product/UI materials, not invented screens. Keep each character consistent across scenes. Full storyboard remains a design reference, not an asset atlas.
- The visual approach is selected per brief: realistic 2.5D layered cutout is a **candidate for digital-product ads**, not a rigid default for documentaries, UGC or physical-product videos.
- When storyboard images are requested, give **one or two reviewable multi-panel images (not a PDF)**, with scenes framed at the requested video ratio; each panel must correspond to a motion plan.
- Do not generate images, audio or video when the owner asks for planning/documentation only. Do not start full production or engine modifications absent scope/approval. A technical proof does not equal creative acceptance.
- Use actual engine structures (GSAP timeline, camera rig, character sprite/rig, scene graph, UI animation, deterministic export) when implementing; avoid poster slides with voice-over.
- Verify **asset provenance, character continuity, actions per beat, correct depth/masking, UI interaction, timing, audio integrity, render/decode and source license** before claiming production succeeds.
- Keep plans, tests, released features, renders and owner acceptance as **separate statuses**. Never invent them.

## What this change does *not* do

This file and the character-first standard are **instructions only**. They do not implement a character sprite generator, pose-consistency checker, 9:16 export, or a new rendering backend. Code changes require specific approval, inspection of the latest source, focused tests and honest result recording. Use regular Git commits for auditable, reversible changes; no secrets or unlicensed media.
