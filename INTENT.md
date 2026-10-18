# INTENT: mise_en_place

> Gets a project ready before the agent starts: templates, asset kits, primitives and context, laid out so the work is just cooking.

Status: placeholder name · written 2026-10-17 from David's direction · **this file changes only when David agrees.**

Scope clarified by David 2026-10-18: not game-specific.

## What it is
- A tool that takes a goal for any kind of project and produces a **prep pack**: chosen starting template, the asset kit, the relevant primitives, and a context brief, all on disk with a `pack.json` manifest. Games are the first use case and the proving demo, not the definition.
- A library of reusable, tested **templates and primitives** it draws from (first pack type: web game templates and game primitives; other pack types such as a data pipeline, dashboard, docs site, CLI tool or napkin component kit are possible later, not planned in detail).
- Deterministic and inspectable: a human can open the pack and see exactly what the agent will start from.

## What it is not
- Not an agent harness or a coding agent (that is bonfire).
- Not the decision model (nibble makes choices; mise_en_place offers the options and assembles the result).
- Not a generator for every language and framework on day one. Pack types are added one at a time, games first, and the design stays domain-agnostic.
- Not the `mise` tool (jdx/mise), which David also uses. Keep the CLI name distinct (e.g. `mep`).

## The proving demo
Given a one-sentence game prompt, `mise_en_place` emits a prep pack that playdough builds a playable game from **with zero setup steps by the agent** (no installs, no scaffolding, no hunting for assets).

## Interface to the stack
Input: goal text + optional constraints. Output: `prep-pack/` with `pack.json` (template id, primitives, assets, brief, open choices for nibble as typed questions). Consumed by bonfire workers and playdough.

## Starting point
Scratch. Salvage only ideas (see docs/salvage.md).

## Open decisions
- Pack format details (draft it in docs/decisions/0001-pack-format.md).
- Where templates/primitives live (in this repo vs a separate catalog).
- Game runtime for the templates (three.js vs Godot; wait for playdough's research).
