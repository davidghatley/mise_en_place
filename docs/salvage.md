# Salvage notes: mise_en_place

Audit date: 2026-10-17. Old repos were read, not modified. This repo's job is to
**do the prep for any project or task (research, generated assets, references,
context) and organize it, so the user or their agents can get straight to the work**.
It ships nothing premade. (Revised 2026-10-19 with INTENT.md; the first draft of this
file assumed premade template packs.)

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
| The finding that packing beats searching | `local-mobile-research@29b6284:experiments/results/R1_ANALYSIS.md` (the short numbers version is in local branch `portfolio-pivot@32e05f2:README.md`, "The finding behind it") | BM25 found 96% of the needed paragraphs, but only about 74% fit in the 1,000-token budget. What helped was a small reranker deciding what goes into the budget. Prep has the same problem: the risk is not failing to find material, it is failing to put the right material in front of the worker. Copy 10–15 lines. |
| Metric: required-item survival per stage | `local-mobile-research@29b6284:experiments/comparability/CONTRACT.md` §3 (the "Required-evidence survival per stage" and "Final evidence recall" rows) | Gives you prep's main metric: of the items the worker actually needed, what fraction were already in the prep folder? Copy the two formulas only. |
| Rule: budgets are counted in real tokens | same file, §2, the "Evidence budget in TOKENS" row | Measure context size with the consuming model's tokenizer, never with a whitespace estimate. One line. |
| Capability contract fields | `primitive@292e991:docs/ontology-v0.md`, "Capability" section (the 7 required fields) | Inputs, outputs, effects, preconditions, postconditions, hard qualifiers, non-goals. A good minimum schema for describing a prep skill. Copy the field list only. |
| Format for open choices in the prep index | Not from an old repo: use Kev's request shape (`vendor/kev` README, "Fine-Tune on Your Own Data": `state` + `questions{type: choice/noul/score, instructions, criteria}`) | Open choices can go to nibble as typed questions. Use Kev's shape directly so nibble needs no translation layer. Don't revive system-a's `shared/typed_decisions` schema. |
| License scope for assets | `primitive@292e991:data/imports/10-three-js.json`, claim `claim:three-js:license:root-mit` and its qualifiers | Code and assets carry separate licences. Every gathered or generated asset needs its own source and licence field in the index. Do not inherit a repo-level license. |

## 2. Lessons

- **Measure what reached the consumer, not what was found.** LMR's biggest result came from logging, at every stage, which required items survived. Build that log in from day one: for every prep folder, record which items the worker actually used.
- **Decide the comparison before building.** LMR computed upfront that its 146-item dev set could only detect differences of about 12 points or more. With a few dozen test tasks, only large wins will show. Plan for that and count small differences as nulls.
- **Hold the consumer fixed.** LMR kept the generator constant so retrieval changes could be measured. Here, pin one worker and vary only the prep.
- **Ontologies grow without limit.** primitive spent its whole V0 on identity, claims and evidence: 46 concepts, 231 claims and 720 evidence links for 10 repos, and little of it helped any task. Start with a flat list and add structure only when a query needs it.

## 3. Leave behind

- **All LMR code** (`substrate/`, `eval/`, `lmr/`) and its 80+ review and ledger docs. It is QA over Wikipedia, not project prep. Its eight-round freeze-review process cost more than the result.
- **LMR's "Mise en Place" README on `portfolio-pivot`.** Copying it would undo the reason for the restart.
- **primitive's SQLite claim graph, schema.sql, vocabulary.json, the 10-repo OSS corpus and the source-audit tooling.** The domain is wrong (general OSS capability mining) and the design is overbuilt for prep.
- **Benchlet tasks.** They are coding-maintenance tasks, not prep tasks.
