# CLAUDE.md

Guidance for Claude Code in this repository.

## What this project is

An agent-based model of a bilingual society, built to study **when, how fast
and why a minority language survives, shifts or erodes, and what policies
change that**.
- **The world:** a **realistic generic society** with two languages, A and
  B. It is not tied to a country, period or calendar years (DEC-08).
- **The reference language pair:** Catalan–Spanish, used for the real lexicon
  and to test the learning core against data. Language pairs generalise
  through parameters (DEC-07).
- **Correlation with a specific society** (Catalonia first) is a later phase.

It is a fresh start that **succeeds the legacy project `bilangsim`**
(`/home/pgerv/personal_projects/abm_bilang_evolution_legacy`, GitHub
`pgervila/bilingual_society_ABM_legacy`). The legacy *ideas* are kept. Its code
is not. This repository is `bilangsim_v2` (DEC-10).

**The model is built in eight layers** (conceptual model §0.1, PROP-12):
1 engine, 2 world, 3 population, 4 activity and contact, 5 language in
society, 6 learning core, 7 observation, 8 scenarios and experiments. Layers
1–4 contain no language. Organisations carry empty language slots that layer 5
fills later. The learning core sees only events, through the interface.

**Current phase: 0, Definition, preparing Phase 1: the agents' world, layers
1–4.** The society is built first, with a simple baseline learner, and the
learning core after (DEC-11). The world layer (geography, settlements,
transport, dwellings, families, organisations such as schools, firms,
hospitals and courts) and the tools to build a world get a full design before
code. There is no code yet. Work happens in `docs/`. See
[`docs/07_roadmap.md`](docs/07_roadmap.md).

Open points are sorted by the phase that needs them. Only those of the next
phase are settled, one at a time. **To resume work, read §0.1 of
[`docs/09_open_points.md`](docs/09_open_points.md).**

## Rules

1. **No legacy code.** Do not copy, port or wrap legacy code. Do not propose a
   `legacy` plug-in, a dependency on the old repository, or comparisons
   against legacy output (DEC-04).
   - Legacy ideas are catalogued in
     `docs/background/modeling_solutions/legacy_best_ideas.md`.
   - The legacy repository may be *read* to understand an idea.
2. **Testable against data** (DEC-02). Every mechanism names:
   - its validation targets ([`docs/04_requirements_and_validation.md`](docs/04_requirements_and_validation.md));
   - the data that calibrates it ([`docs/05_data_inventory.md`](docs/05_data_inventory.md));
   - a published model it is based on.

   Every parameter goes into the parameter register, with its source or
   prior. Acceptance bands are fixed **before** fitting.
3. **Start simple, on a scientific basis** (DEC-03). Minimal first versions.
   Approaches with emergent structure (self-organising maps, neural agents)
   are research tracks that must beat the specified ones on held-out targets.
4. **The learning model comes before policy** (DEC-01). The society is
   *built* first (DEC-11), but no policy conclusion is drawn before the
   learning core passes its gate.
5. **Same experience, same result.** Time is measured in days, events are
   timestamped, and random streams are keyed by agent, purpose and event.
   Results must not depend on how work is chunked or ordered.
6. **Decisions belong to Paolo.** Open questions (**Q-xx**) and proposals
   (**PROP-xx**) in [`docs/06_decisions.md`](docs/06_decisions.md) are
   decided by Paolo.
   - Recommend, but do not settle them silently.
   - Record each decision with its date and reason.
7. **Background documents are frozen** (`docs/background/`). Record changes of
   mind in the living documents (`docs/01`–`08`) and in the decision log.
8. **Data.** Never commit raw data. Each resource gets a manifest entry
   (source, version, licence, checksum). Check licences before use.
9. **Generic first, general through parameters** (DEC-07, DEC-08).
   - No culture-specific facts in code.
   - Anything specific to a language pair or a society is data or a
     parameter.
   - The social layer uses the labels A and B.
   - At the collective level, v1 targets generic stylised facts (V31–V36).
     Census and survey calibration belong to the specific-society phase.
10. **Motives, not loyalty** (DEC-09). Transmission and language choice
    follow proficiency, perceived status and defence (attachment × perceived
    threat). Perceptions are built from each agent's experience
    ([`docs/specs/motives_and_transmission.md`](docs/specs/motives_and_transmission.md)).

## Tooling

- **`uv` manages every Python interpreter and environment** (DEC-06). There is
  no bare `python` on PATH: use `uv run …`.
- The proposed stack (PROP-03, not yet confirmed):
  - Python 3.13, NumPy, Numba for hot kernels;
  - Parquet for tables, Zarr for snapshots, JSON run manifests;
  - pytest plus the validation harness in CI;
  - `sbi` and SALib for calibration and sensitivity analysis.

## Writing documents

- Plain English, short sentences, tables for comparisons.
- References follow the conventions in the glossary §1 ([`docs/08_glossary.md`](docs/08_glossary.md)): short names for documents, `§` for sections, prefixed IDs where they clash.
- **Define every key concept** in the glossary when it is first used, in a document or in discussion. The structure of the model is defined in the glossary §2, and the terms of time in §3.
- Stable IDs:
  - DEC/PROP/Q for decisions;
  - R for requirements;
  - V for validation targets;
  - SM for submodels;
  - F1–F5 for language features;
  - domain codes (HOME, SCHOOL, WORK, …).

  Never reuse an ID with a new meaning.
- Full references at the end of each document. Mark unverified facts
  *(to check)*.
- Each document starts with a status line (draft or version, and date).

## Document map

| File | Content |
|---|---|
| [`docs/01_vision_and_scope.md`](docs/01_vision_and_scope.md) | purpose, research questions, principles P1–P12, scope, success criteria |
| [`docs/02_society_domains.md`](docs/02_society_domains.md) | the domains of social life, with participants, norms, policy levers and data |
| [`docs/03_conceptual_model.md`](docs/03_conceptual_model.md) | ODD overview: the eight layers (§0.1), entities, scales, language pairs as parameters, schedule, design concepts, submodels SM-01–SM-16, interface, scaling |
| [`docs/04_requirements_and_validation.md`](docs/04_requirements_and_validation.md) | R1–R14, V1–V36, hypotheses H1–H3, calibration protocol, invariance tests, parameter register |
| [`docs/05_data_inventory.md`](docs/05_data_inventory.md) | resources, data to collect, the first inventory task |
| [`docs/06_decisions.md`](docs/06_decisions.md) | decision log (DEC, PROP, Q) |
| [`docs/07_roadmap.md`](docs/07_roadmap.md) | phases 0–7 and their gates; the society first (DEC-11) |
| [`docs/08_glossary.md`](docs/08_glossary.md) | how to read references (§1); layers and objects (§2); time (§3); other terms (§4) |
| [`docs/09_open_points.md`](docs/09_open_points.md) | every open point, sorted by the phase that needs it; where we are (§0.1) |
| [`docs/specs/`](docs/specs/) | submodel specifications, written before code. So far: [`motives_and_transmission.md`](docs/specs/motives_and_transmission.md) (SM-16, SM-03) |
| [`docs/background/`](docs/background/README.md) | frozen analyses from the legacy repository: the memory model, the redesign proposal, its review, embeddings, the five language features, legacy ideas |

## Other folders

`/home/pgerv/personal_projects/abm_bilang_evolution` is an unrelated
experiment from May 2026 (a minimal NumPy/C++ benchmark kernel). It is not
part of this project.
