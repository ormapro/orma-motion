---
name: orma-motion
description: Panduan produksi Orma Motion untuk motion graphic, explainer, iklan produk, storyboard berbasis voice-over, perencanaan karakter dan aset, GSAP animation, serta quality control anti-slide/PPT. Gunakan saat user meminta membuat atau memperbaiki video motion, animatic, storyboard, atau audit engine Orma Motion.
license: MIT
metadata:
  author: OrmaPro
  version: "0.1.0"
  upstream: "Bang Motion v1.19.0 by Bang Tutorial (MIT)"
---

# Orma Motion — Production Skill

This skill is the **Orma Motion workflow** packaged with the source and examples of **Bang Motion v1.19.0**. Maintain Bang Tutorial attribution and the repository LICENSE.

## Read first, based on the actual task
1. Read `../../AGENTS.md` for the Orma standards and scope.
2. For video using characters, read `../../docs/ORMA_MOTION_CHARACTER_FIRST_WORKFLOW.md` before generating any assets.
3. Read `../../SKILL.md` for the upstream Bang Motion motion grammar, then `../../references/anti-ppt.md` and only the relevant references.
4. For actual engine behavior, inspect `../../assets/starter-*.html`, `../../scripts/`, and `../../references/architecture.md`. Do not confuse these starters with a completed Orma Motion application.
5. Use `references/ASSET_INDEX.md` to select from the packaged gallery and HTML starters. Gallery images are style references, not production-ready layered character assets.
6. For live project status and decisions, use the connected GitHub tool where available: coordination source `omar-mcht/orma-member-area/docs/motion/README.md`, technical source `ormapro/orma-motion`. A packaged ZIP is a snapshot, **not automatic GitHub synchronization**.

## Workflow — ask only for essential missing inputs
- Understand purpose, target audience, product, existing HTML/source, supplied media, exact VO/audio, format and constraints. Do not invent product interfaces or features.
- Analyze the **complete VO**, duration and all beats before creating a storyboard or asset.
- Make each beat meaningful: visible change, action, subject/object, continuity, camera, transitions, timing and method. Text and visuals should support one another; avoid decorative microtext or labels like “illustration of ...”.
- For character-led work prepare **Character Asset Sheet**, pose/expression/action matrix, **Set & Prop Inventory**, full-video asset manifest and reusable IDs **before asset generation**.
- Keep foreground, character, midground, backgrounds, props and UI independent. Do not crop a composite/storyboard poster and call a zoomed cutout a character rig.
- Choose an appropriate visual strategy per brief (2D, layered 2.5D, documentary, UGC/hybrid footage, UI, or typography). Realistic 2.5D is a possible strategy, **not a mandatory default**.
- During real production use layered assets with meaningful object/character actions, deterministic GSAP timelines, synced VO/SFX where supplied, transitions and camera movement. Moving the camera alone is not enough.
- Use **30 FPS minimum** for final output, default 30. Preserve requested aspect ratio/duration; the current upstream export example is landscape-oriented and needs adaptation for portrait.
- QA: visual clarity, scene continuity, audio timing, asset source/license, expected actual animations, frame rate/decoded frames, and MP4 integrity. Show separate statuses for planned, assets ready, motion tested, rendered, owner approved.
- If user asks for a visual storyboard, render **one or two readable image sheets**, not a PDF, unless they specifically request PDF. If user asks only for planning, do not generate media or change engine code.

## Tool limits and honesty
The skill teaches workflow; it does not install a GPU renderer, external model, After Effects bridge or MP4 export runtime automatically. Use tools actually available. Never claim an animation, render or live synchronization succeeded without inspection or a real test.

## Upstream and provenance
`../../SKILL.md`, `../../references/`, `../../assets/starter-*.html`, and `../../scripts/` come from Bang Motion (Bang Tutorial, MIT). `../../docs/BANG_MOTION_UPSTREAM_README.md` preserves the original README.
