<div align="center">

<img src="assets/orma-motion-icon.svg" width="112" alt="Orma Motion logo">

# Orma Motion

**Motion graphics production skill and plugin for ChatGPT, Codex and compatible agents.**

Storyboard · Character Asset Sheet · Set & Prop Inventory · Visual direction · GSAP motion · Anti-slide QA

[Production skill](skills/orma-motion/SKILL.md) · [Gallery](docs/gallery/) · [HTML starters](assets/) · [Technical workflow](docs/ORMA_MOTION_CHARACTER_FIRST_WORKFLOW.md)

</div>

## Start here

**Orma Motion** is the OrmaPro production workflow, currently built on **Bang Motion v1.19.0 by Bang Tutorial (MIT)**. This repository preserves the original Bang Motion examples, images, scripts and references while packaging Orma production standards for use from ordinary ChatGPT conversations.

- **ChatGPT Plugin:** the portable package identity is in [`plugin.json`](plugin.json); the skill is under [`skills/orma-motion/`](skills/orma-motion/). Its name is **Orma Motion**, not Bang Motion.
- **Installable source ZIP:** use **Code → Download ZIP** in this GitHub repository. The archive contains the plugin, logo, gallery JPGs, starter HTML files and all reference documents.
- **Agent entrypoint:** [`AGENTS.md`](AGENTS.md) and [Orma Motion production skill](skills/orma-motion/SKILL.md).
- **Visual examples:** [13 gallery JPGs](docs/gallery/). These are style references, not pre-rigged animation assets.
- **Core engine source:** root [`SKILL.md`](SKILL.md) is the preserved upstream Bang Motion v1.19.0 workflow; `assets/starter-*.html`, `references/`, and `scripts/` are the reference implementation.
- **Production status:** no claim of fully automated VO-to-MP4 orchestration, asset generation, or completed portrait renderer. Read the actual code and QA before claiming a capability works.

### Install in ChatGPT

Install the package as **a new private Plugin named Orma Motion**, using the repository ZIP and the available ChatGPT upload / Plugin Creator flow. The previously installed **Bang Motion** private plugin is a separate package and is **not automatically renamed or updated** when this GitHub repo changes. Verify the new plugin after installing it.

### License and original source

This repository carries the original Bang Motion materials, licensed under the [MIT license](LICENSE), with **Copyright (c) 2026 Bang Tutorial** retained. Orma Motion branding and workflow adaptations are separate from that upstream authorship.

The original, complete Bang Motion README is preserved without deletion at [`docs/BANG_MOTION_UPSTREAM_README.md`](docs/BANG_MOTION_UPSTREAM_README.md); upstream source: https://github.com/bangtutorial/bang-motion.

### Development and scope

Administration, handoff and decisions are coordinated in `omar-mcht/orma-member-area/docs/motion/README.md`. Technical source, plugin, references and engine reside here. GitHub updates are not automatically pushed into previously installed plugin releases. Use the latest code and explicit permission before changes or deployment.
