# Salvage notes: mise_en_place

Audit date: 2026-10-17. Old repos were read, not modified. This repo's job is to
**prepare a project so an agent can finish a task with no setup work**. The proving
demo is: game prompt in, "prep pack" (templates, asset kits, primitives, context) out,
and playdough builds from that pack with zero setup.

No old repo built this. The name was used once, by mistake, as the README title on
local-mobile-research's unpushed `portfolio-pivot` branch. That project is an offline
QA app. **Do not inherit its framing.**

## How to bring anything in

Copy only the excerpt you need into `docs/reference/<name>.md`, with this header:

```text
> Provenance: davidghatley/<repo>@<commit>:<path> (copied 2026-10-17, excerpt)
> Status: reference only. Not a spec. Overridden by anything in this repo.
```

Never copy code wholesale. Rewrite anything you need against this repo's own spec.

## 1. Carry as reference

| What | Source | Why |
|---|---|---|
| The finding that packing beats searching | `local-mobile-research@29b6284:experiments/results/R1_ANALYSIS.md` (the short numbers version is in local branch `portfolio-pivot@32e05f2:README.md`, "The finding behind it") | BM25 found 96% of the needed paragraphs, but only about 74% fit in the 1,000-token budget. What helped was a small reranker deciding what goes into the budget. Prep has the same problem: the risk is not failing to find a template or primitive, it is failing to fit the right ones into the pack. Copy 10–15 lines. |
| Metric: required-item survival per stage | `local-mobile-research@29b6284:experiments/comparability/CONTRACT.md` §3 (the "Required-evidence survival per stage" and "Final evidence recall" rows) | Gives you the pack's main metric: of the items the build actually needed, what fraction ended up in the pack? Copy the two formulas only. |
| Rule: budgets are counted in real tokens | same file, §2, the "Evidence budget in TOKENS" row | Measure context-pack size with the consuming model's tokenizer, never with a whitespace estimate. One line. |
| Capability contract fields | `primitive@292e991:docs/ontology-v0.md`, "Capability" section (the 7 required fields) | Inputs, outputs, effects, preconditions, postconditions, hard qualifiers, non-goals. A good minimum schema for a primitive card. Copy the field list only. |
| Format for the "open choices" in `pack.json` | Not from an old repo: use Kev's request shape (`vendor/kev` README, "Fine-Tune on Your Own Data": `state` + `questions{type: choice/noul/score, instructions, criteria}`) | INTENT says pack.json carries open choices for nibble as typed questions. Use Kev's shape directly so nibble needs no translation layer. Don't revive system-a's `shared/typed_decisions` schema. |
| License scope for assets | `primitive@292e991:data/imports/10-three-js.json`, claim `claim:three-js:license:root-mit` and its qualifiers | three.js code is MIT, but example assets carry their own licenses. Every asset in an asset kit needs its own license field. Do not inherit a repo-level license. |

## 2. Lessons

- **Measure what reached the consumer, not what was found.** LMR's biggest result came from logging, at every stage, which required items survived. Build that log into prep packs from day one: for every pack, record which items playdough actually used.
- **Decide the comparison before building.** LMR computed upfront that its 146-item dev set could only detect differences of about 12 points or more. With a few dozen game prompts, only large wins will show. Plan for that and count small differences as nulls.
- **Hold the consumer fixed.** LMR kept the generator constant so retrieval changes could be measured. Here, pin one playdough build path and vary only the pack.
- **Ontologies grow without limit.** primitive spent its whole V0 on identity, claims and evidence: 46 concepts, 231 claims and 720 evidence links for 10 repos, and none of it is game-relevant. Start with a flat list of primitive cards and add structure only when a query needs it.

## 3. Leave behind

- **All LMR code** (`substrate/`, `eval/`, `lmr/`) and its 80+ review and ledger docs. It is QA over Wikipedia, not project prep. Its eight-round freeze-review process cost more than the result.
- **LMR's "Mise en Place" README on `portfolio-pivot`.** Copying it would undo the reason for the restart.
- **primitive's SQLite claim graph, schema.sql, vocabulary.json, the 10-repo OSS corpus and the source-audit tooling.** The domain is wrong (general OSS capability mining) and the design is overbuilt for game primitives.
- **Benchlet tasks.** They are coding-maintenance tasks, not prep tasks.
