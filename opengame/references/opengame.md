# OpenGame project notes

Source: https://github.com/leigest519/OpenGame (main branch, reviewed 2026-11-18). This is a compact interpretation of the repository, not a bundled copy of its runtime or templates. Consult the source for current behavior.

## What the project contains

OpenGame extends a qwen-code-derived agent runtime for prompt-to-web-game creation. Its README describes Game Skill as Template Skill plus Debug Skill; GameCoder-27B is a separate specialized model. The README says the OpenGame-Bench evaluation pipeline is forthcoming, so do not imply it is installed or claim official scores.

`agent-test/templates/core` provides a base, and `templates/modules` contains five Phaser archetypes: `platformer`, `top_down`, `grid_logic`, `tower_defense`, and `ui_heavy`. `agent-test/docs/modules/<type>/` supplies design rules and template APIs. Read the matching module and implementation when using the actual template. `agent-test/docs/debug_protocol.md` covers integration checks; `asset_protocol.md` covers the project's own asset tooling. `template-skill/` contains an evolution pipeline for deriving and maintaining template families from completed games; it is a project component, not automatic learning provided by this Codex skill.

## Design and integration

- Platformer: movement, collision, camera, levels and character state; check exact tile layer names and level order.
- Top-down: movement and aiming, collisions and camera; distinguish an arena background from a tilemap with floor and wall layers.
- Grid logic: model board state separately from rendering; handle valid moves, turns, animation completion and end states.
- Tower defense: path, wave progression, placement validity, attack targeting and victory/defeat.
- UI-heavy: dialogue, cards, quizzes or turn-based interactions; check focus, event wiring, turn completion, overlay depth and accessible controls.

In Phaser projects check scene key registration against transitions; compare actual configuration fields with callers; ensure asset manifests, files, textures, animation frame keys and code references agree. For subclass hooks, inspect the base class for real names, signatures and visibility. For restart, reset state and clean up listeners and dynamically created objects. Apply these checks only when relevant to the chosen architecture.

## Using OpenGame itself

The repository README specifies Node.js 20+, source installation (`npm install`, `npm run build`, `npm link`), and `opengame -p "..."` for headless operation. Follow the current README and inspect installed CLI options before running. The README notes headless mode permits edits; `--yolo` also permits shell commands, so do not add it automatically. When running outside its expected directory, the README documents `GAME_TEMPLATES_DIR` and `GAME_DOCS_DIR`. Its runtime uses an OpenAI-compatible API and separate optional asset provider configurations; credentials and potential provider charges are external prerequisites. Never print secrets. The `.qwen` settings paths are a compatibility detail and can change.

The project's own integration test guide requests external provider keys and invokes a full agent pipeline; do not treat it as an offline smoke test. Its debug protocol's prohibition on installation assumes an already-prepared environment, not a general rule: install dependencies when the actual project needs them.

## Validation

Build and test with the actual project's scripts; use browser interaction and console/network inspection for behavior and visual checks. Verify claims against observed evidence, including what was not exercised. A successful compile alone does not prove that the game is playable.
