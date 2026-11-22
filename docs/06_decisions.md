# Decisions

> **Status:** living log, started Nov 2026.
> - **DEC** entries are decided.
> - **PROP** entries are proposals with no objection yet, awaiting confirmation.
> - **Q** entries are open questions, with options and a recommendation.
> - The **open points** document ([`09_open_points.md`](09_open_points.md))
>   lists every open point by area of modelling, in the order we settle them.
>
> When a question is settled, move it to DEC with the date, who decided and
> why. Do not delete superseded entries; mark them superseded.

---

## 1. Decided

| ID | Decision | Date and source | Why |
|---|---|---|---|
| DEC-01 | **The learning model comes before policy work.** | 2026-11-08, Paolo | "Useless if the learning model is weak": policy conclusions inherit every distortion of the learning core. |
| DEC-02 | **The learning model must be testable with data that exists or can be collected.** | 2026-11-08, Paolo | A precondition for a useful and reliable model |
| DEC-03 | **Start simple but accurate**: a minimal first implementation on a modern scientific basis. Start on modest hardware, scale "very far" later. | 2026-11-08, Paolo | — |
| DEC-04 | **A fresh repository, with no legacy code**, not even as a plug-in or comparison baseline. Keep the legacy *ideas*. Validate against data, not against legacy output. | 2026-11-21, Paolo | "Keep the good ideas … and integrate them into a more powerful and reliable implementation." |
| DEC-05 | **Keep all good ideas of the legacy model, including its key domains of society** (family, school, work, friends and so on), and extend them. | 2026-11-21, Paolo | See [`02_society_domains.md`](02_society_domains.md) and [`background/modeling_solutions/legacy_best_ideas.md`](background/modeling_solutions/legacy_best_ideas.md) |
| DEC-06 | **`uv` manages every Python interpreter and environment.** | carried over from the legacy project, Paolo | Project convention |
| DEC-07 | **Catalan–Spanish is the first reference pair, but the model generalises through parameters.** Every property of a language pair (lexicon, frequencies, form overlap) and every property of a language's social position (status, institutional support, share of speakers) is data or a parameter, never a hard-coded assumption. The social layer uses neutral labels A and B. (Answers Q-01.) | 2026-11-21, Paolo | "Catalan/Spanish is OK, but it would be better to be able to generalize via parameters." |
| DEC-08 | **A realistic generic world first; correlation with a specific society later.** Build a world that is realistic in structure (demography, households, domains, schedules, networks) with parameters in plausible ranges, not tied to a country, period or calendar years. The learning and memory models are still tested against real data from the start. At the collective level, stay general: the targets are generic stylised facts. Calibration to a specific society (e.g. Catalonia, census, EULP) is a later phase. (Answers Q-03.) | 2026-11-21, Paolo | "I would not start with super real conditions or specific years … I'd like to stay general at the beginning, not too coupled to a specific cultural reality." |
| DEC-09 | **Transmission follows realistic motives, not a "loyalty" trait.** Parents pass on the language they are most proficient in, the one they perceive as more prestigious, or the one they want to defend against assimilation. These motives rest on perceptions built from each person's experience. Specification: [`specs/motives_and_transmission.md`](specs/motives_and_transmission.md). (Answers Q-05.) | 2026-11-21, Paolo | "Most of the times people pass the language they are most proficient with, or the one they perceive as more prestigious, or the one they perceive they want to defend against assimilation." |
| DEC-10 | **The project repository is named `bilangsim_v2`** (the local folder, from 2026-11-22). The package name is still open. (Partly answers Q-02.) | 2026-11-22, Paolo | Paolo's choice. The name follows the legacy `bilangsim`. |

---

## 2. Proposed, awaiting confirmation

| ID | Proposal | Rationale | Where |
|---|---|---|---|
| PROP-01 | **Approach A (grounded lexical memory) is the first learning core.** B (developmental connectionist) and C (neural agents) are research tracks that must beat A on held-out targets. A simple **baseline learner** is the yardstick for all of them. | Testable on a laptop, interpretable, grounded in published models | LMNA §7; conceptual model §8 |
| PROP-02 | **No vector databases. Embeddings only behind the five-condition gate.** | They add nothing to reliability; explicit statistics are affordable at this lexicon size | `embeddings_and_vector_databases.md` |
| PROP-03 | **One repository**, with the social layer and the learning core behind an interface. Python 3.13, NumPy, Numba for hot kernels (Rust only if profiling demands it). Parquet for tables, Zarr for state snapshots, JSON run manifests. pytest plus the validation harness in CI. | Continuity with the stack that worked; performance where needed | LMNA §3.9, §4.11 |
| PROP-04 | **Time.** Learning events are timestamped in **days**. The social scheduling step is **one week**, with events placed on actual days. Demography runs in monthly substeps. | Same experience, same result (P4); social cost per week, learning resolution per day | conceptual model §2.2 |
| PROP-05 | **Space.** Municipalities, with districts for large cities, as nodes with distances. Settings inside them. No grid. | What matters is who shares which setting | conceptual model §2.2; domains document §6 |
| PROP-06 | **Language choice** resolved in a fixed order: institutional norm, relationship memory, then a **motive-weighted choice** (accommodation and MAXIMIN, status, defence) among the languages the group can follow, receptive mode, initiator, exclusion. Agents use **perceived profiles** of each other. *(Revised 2026-11-21 for DEC-09.)* | Keeps the legacy MAXIMIN and stickiness; makes accommodation realistic; uses the same perceptions as transmission | domains document §4.1–4.2; motives spec §6 |
| PROP-07 | **Initial conditions by spin-up and burn-in.** Each agent's knowledge comes from the same learner run through a personal history. In the generic world (DEC-08), those histories come from a **burn-in** of the world itself under a baseline scenario. Histories specific to each birth cohort come only in the specific-society phase. *(Revised 2026-11-21.)* | Removes the legacy initial-conditions mismatch (M13) without needing historical data | conceptual model §5 |
| PROP-08 | **A specification document before code** for every submodel; the ODD description kept up to date; a parameter register | Principles P1, P5 | validation document §5 |
| PROP-09 | **Measurement through virtual instruments**: census, EULP, test battery | Outputs in the units of real data (R1, R10) | conceptual model §4 |
| PROP-10 | **The motives model** of [`specs/motives_and_transmission.md`](specs/motives_and_transmission.md). Perceived status, perceived vitality and threat, and attachment, all built from experience. A logit choice among A, B or both for transmission. The same perceptions, with separate weights, in everyday choice. | Implements DEC-09 with endogenous, measurable perceptions | motives spec |
| PROP-11 | **A synthetic language-pair generator.** Pairs are generated from parameters (lexicon size, frequency structure, share of cognates and distribution of form distances), so results can be swept over linguistic distance (RQ6). The generator is checked by reproducing results of the real Catalan–Spanish pair with parameters matched to it. | Implements DEC-07; the language-similarity parameter of Mira & Paredes (2005) made concrete | conceptual model §2.3 |

---

## 3. Open questions

### Q-01 — Reference language pair

- **Options:**
  - (a) Catalan–Spanish only;
  - (b) Catalan–Spanish, plus a distant pair later (e.g. Basque–Spanish) to
    test generality (RQ6);
  - (c) start with a distant pair.
- **Recommendation: (b).** Catalan–Spanish has the richest data, and the
  legacy model already targeted it.
- **Decision:** **DEC-07** (2026-11-21). Catalan–Spanish first, with
  generalisation through parameters.

### Q-02 — Project and package names

- **Options:** keep the working folder name `bilingual_society_abm`, with a
  short package name chosen when the repository is created.
- **Recommendation:** the GitHub repository `bilingual_society_ABM`, mirroring
  the legacy `bilingual_society_ABM_legacy`. A package name different from the
  legacy `bilangsim`.
- **Decision:** partly, **DEC-10** (2026-11-22). The repository is `bilangsim_v2`. The package name is still open.

### Q-03 — Start year and historical run

- **Options:**
  - (a) Y0 = 1986, the first census language data, with each person's state
    spun up from cohort histories;
  - (b) Y0 = 1940, simulating the population's history itself;
  - (c) Y0 = today, projections only.
- **Recommendation: (a)** for v1. It validates against 1986–2023, with
  hold-out of recent waves. Try (b) later as a robustness check. (c) cannot be
  validated.
- **Decision:** **DEC-08** (2026-11-21). None of these for now: a realistic
  generic world first, without calendar years. Options (a) and (b) come back
  in the specific-society phase.

### Q-04 — Literacy in v1

- **Options:**
  - (a) v1, because the census asks about reading and writing;
  - (b) v2, with v1 outputs limited to understanding and speaking.
- **Recommendation: (b).** Literacy is a separate channel with its own
  exposure and tests.
- **Decision:** —

### Q-05 — Attitudes and identity

- **Options:**
  - (a) none in v1;
  - (b) a single latent **language-loyalty** trait in v1, correlated within
    families, acting on the transmission decision and on language choice, and
    calibrated on EULP identification and attitude items;
  - (c) a full utility model in v1, weighing economic payoff against identity
    (the legacy "pride vs interest" idea).
- **Recommendation: (b).** Transmission and choice among capable bilinguals
  probably cannot be fitted without some attitude term. A full utility model
  waits for v2.
- **Decision:** **DEC-09** (2026-11-21). Not a loyalty trait. Instead, three
  motives (proficiency, perceived status, defence against assimilation) built
  on perceptions from experience. See PROP-10.

### Q-06 — Contact and grammar stage

Should the stage with lexical variants and grammatical variables (F5,
V21–V23) be on the roadmap as v3?

- **Recommendation: yes.** Collect its data early, through the acceptability
  module of the online study.
- **Decision:** —

### Q-07 — Our own data collection

Should we run the online vocabulary and language-history study, with the
listening and acceptability modules?

- **Recommendation: yes.** Start the design and the ethics application in
  Phase 1, because the lead time is long.
- **Decision:** —

### Q-08 — Memory rule

- **Options:** a bake-off on V1–V5 and V10, plus cost, between:
  - ACT-R with Pavlik–Anderson decay (time unit fixed, review N1);
  - the multiscale context model;
  - FSRS;
  - the Predictive Performance Equation.
- **Recommendation:** run the bake-off, with V3 (permastore) as a gating
  test. Do not pre-commit to ACT-R.
- **Decision:** —

### Q-09 — Lexicon size for A0

- **Options:**
  - (a) 5,000 lemmas per language (LMNA);
  - (b) 20,000–30,000, with sparse storage.
- **Recommendation:** decide after the data inventory. Adult tests probably
  need (b) (review N11).
- **Decision:** —

### Q-10 — Hosting and licence

- **Options:**
  - (a) a public GitHub repository with a permissive licence for code (MIT or
    BSD-3), plus a separate data policy per resource;
  - (b) private until the first results.
- **Recommendation:** decide before any data-derived table is committed.
  Some sources (Apertium GPL, SUBTLEX terms) may constrain what can be
  redistributed.
- **Decision:** —

### Q-11 — Default semantics in A1

- **Options:**
  - semantics option S1: explicit per-setting frequencies, MCR domain labels, PPMI;
  - semantics option S2: embeddings.
- **Recommendation: S1.** S2 only if it passes the gate and the three-way
  experiment.
- **Decision:** —

### Q-12 — Population scaling

- **Options** (conceptual model §9):
  - A: a synthetic region at reduced scale;
  - B: one real area at 1:1;
  - C: several contrasting real areas at 1:1.
- **Recommendation: A** for v1, C for v2 if scaling artefacts matter. Since
  DEC-08, A is the natural choice: a synthetic generic region whose
  municipality sizes follow a realistic distribution. B and C become options
  for the specific-society phase.
- **Decision:** —

### Q-13 — When to build the social layer

- **Options:**
  - (a) after A0 passes its single-agent gate;
  - (b) in parallel, using the baseline learner.
- **Recommendation:** write the social-layer specifications in parallel
  (Phases 1–2). Implement after the A0 gate, consistent with DEC-01. The
  exposure model for A0 uses scripted histories, so it does not need the
  social layer.
- **Decision:** —
