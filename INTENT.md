# INTENT: mise_en_place

> Give it the project or task you're about to start. It does the prep (research, assets, references, context) and lays everything out, organized, so you or your agents can get straight to the work.

Status: placeholder name · rewritten 2026-10-19 from David's direction · **this file changes only when David agrees.**

David, 2026-10-19: "the user should be able to give it a project or task that they are working on or want to build and the agent should get everything prepped and organized for the user or the user's agents to complete that task."

## What it is
- **An agent, or a set of skills an agent uses, that does the prep for a task.** The input is a project or task in the user's own words, plus whatever already exists (a repo, a folder, notes). The output is that task's prep, made fresh for it and organized in one place.
- **Prep is work done, not things handed over.** Examples of what it might do for a task, depending on what the task needs:
  - research: search and SEO research, competitors, prior art, docs for the libraries in play;
  - assets: generate the images, icons, diagrams, sample data or copy drafts the task will need, with the tools on the machine (ComfyUI, three.js, Blender, the secret-sauce workshop);
  - references: pull relevant material from the user's own libraries (fridge, pantry, research corpus) and the web;
  - context: read the existing project and write down what a worker needs to know;
  - organization: put it all into a clear layout with an index that says what each thing is, where it came from, and what is still open.
- **Project-agnostic.** Nothing in it is specific to one kind of project. The same agent preps a landing page launch, a data analysis, a research paper, a design system or anything else.
- **Inspectable.** The user can open the prep and see what was made, why, and from which sources, before any work starts.

## What it is not
- Not a template, starter kit or "agent in a box". It ships with **no premade assets, templates, code blocks or packs**. Everything it hands over was made or gathered for the task in front of it.
- Not the worker. It doesn't build the thing; it gets the station ready for whoever does (the user, Claude Code, bonfire or any other agent).
- Not specific to any domain. Never describe it by one use case.
- Not the decision model (nibble) or the harness (bonfire). It can use them.
- Not the `mise` tool (jdx/mise). Keep the CLI name distinct (e.g. `mep`).

## The proving demo (proposed)
Give it two unlike tasks, for example "launch a landing page for nibble" and "analyse a year of my bank exports". For each, it produces an organized prep folder whose research, generated assets and context the worker actually uses, and the worker (a person or an agent) starts on the task without doing its own setup research. Measure what fraction of the prep the worker used, and what it had to go and find itself.

## Interface to the stack
Input: task text + optional paths to existing material. Output: a prep folder with an index (what each item is, its source, what's open). Open choices can be written as typed questions for nibble. Any worker can consume it; bonfire can run prep as a job.

## Starting point
Fresh. The first build (branch `feat/core`, 2026-10-18) followed the old intent: a library of premade templates and blocks for one kind of project, assembled into packs. It is archived at tag `archive/prep-pack-v0` as a record, not a base. Ideas still worth keeping: inspectable output, an index that names sources, logging which prep items the worker used.

## Open decisions
- Agent, skill set, or both (e.g. a Claude Code agent that calls small prep skills).
- Prep folder layout and index format.
- Which prep skills come first (research and asset generation are the likely pair; the per-repo SEO research done on 2026-10-18 is an example of one).
