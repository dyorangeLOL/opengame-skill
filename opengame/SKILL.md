---
name: opengame
description: Build, improve, or debug playable browser games using OpenGame-inspired genre templates, cross-file integration checks, and interactive validation. Use for web game creation or for working with the OpenGame framework; do not assume its CLI, model, or asset tools are installed.
---

# OpenGame: browser game development

Turn the user's game idea into a playable browser game. Preserve an existing project's engine and conventions unless the user requests a change. For OpenGame-specific setup, archetypes, and debugging, read [references/opengame.md](references/opengame.md).

## Workflow

1. Identify the player goal, core loop, controls, win/loss conditions, visual direction, target device, and constraints from the request. Make reasonable assumptions; resolve only essential ambiguity. Choose a small playable vertical slice before expanding features.
2. Choose an architecture suited to the mechanics and the existing project: simple Canvas for small games; Phaser for 2D scenes, physics and asset management; another engine only when appropriate. Map platformer, top-down, grid logic, tower defense, or UI-heavy interactions to a suitable structure. For OpenGame templates inspect the actual files and APIs before extending them; do not invent hooks or assume every template is installed.
3. Implement an end-to-end loop: entry/start, controls, visible feedback, progression, terminal state, and restart. Keep configuration, scene transitions, input, asset keys, and entity ownership consistent across files. Reset mutable state and remove listeners/timers on scene shutdown or restart.
4. Plan assets by function and visual consistency. Use existing or locally generated placeholders when suitable; replace with requested assets as available. OpenGame's asset-generation and tilemap tools are specific to its runtime, not generic Codex tools. Check availability and cost before relying on external providers; never claim generated assets exist without verifying files.
5. Run the project's appropriate build and tests. Launch the game and exercise real interactions in a browser where available: start, core controls, one representative progression, win/loss, and restart. Inspect console and network errors, visual clipping, input and asset loading. Fix observed causes, then repeat affected checks. For complex games report precisely which flows were exercised and any remaining gaps. If browser interaction is unavailable, say so rather than claiming playability.
6. Judge the result along three practical dimensions inspired by OpenGame-Bench: build/runtime health, visual usability, and alignment with the requested gameplay. These checks are an adaptation, not an official benchmark score.

When diagnosing errors, read the complete message and inspect the referenced file. Check imports, type definitions, object initialization, registered scene names, config paths, asset and animation keys, then fix the underlying cause. Avoid changing dependencies as a reflex. Record reusable fixes only when verified and within the user's authorized scope.
