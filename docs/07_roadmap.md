# Roadmap

> **Status:** draft v2 (2026-11-22), for discussion. It follows three
> decisions:
> - **DEC-01:** the learning model before policy;
> - **DEC-08:** a realistic generic world first, and correlation with a
>   specific society later;
> - **DEC-11:** the society, the agents' world, is built first, with the
>   baseline learner. The learning core comes after.
>
> Each phase ends at a **gate**: an explicit check that must pass before the
> next phase starts. Hardware tiers come from LMNA §4.11. The open points are
> sorted by the phase that needs them in
> [`09_open_points.md`](09_open_points.md). The phases build the **layers** of
> the model (conceptual model §0.1, PROP-12; terms in the glossary §2–§3).

---

## Overview

| Phase | Goal | Hardware | Gate |
|---|---|---|---|
| **0. Definition** (now) | Settle what Phase 1 needs, and write the specifications of layers 1–4 | — | the points of open points §1–§4 settled; the specifications of layers 1–4 written |
| **1. The agents' world** | Layers 1–4: the engine; the world (territory, settlements, transport, dwellings, organisations) and the tools to build it; the population; activity and contact. No language yet. | laptop | generated worlds and populations within plausible ranges; the step update within its performance budget and invariant to bookkeeping |
| **2. Language in society** | The interface and the baseline learner; language choice; perceptions, motives and transmission; the virtual census and survey | laptop, then workstation | the motives model's unit tests; first qualitative patterns with the baseline learner |
| **3. Learning core** | Lexicon of the real pair, exposure model v0, test battery and single-agent harness (3a); then the learner A0 (3b) | laptop | A0 passes its bands **against real data** and beats the baseline learner (LMNA D1) |
| **4. Generic world** | A0 replaces the baseline learner in the society: burn-in, generic stylised facts, sweeps over parameters, exploration of policy levers | workstation; cluster for sweeps | V31–V36 reproduced across plausible ranges |
| **5. Extensions** | Domain semantics, literacy, administration, richer motives, richer media, a second real language pair, contact and grammar; research tracks B/C | as needed | per extension (LMNA D3 for B/C) |
| **6. Specific society** | Correlation with one real society (Catalonia first): census population, cohort histories, calibration with hold-out waves | workstation and cluster | V17, V24–V28 on hold-out waves (LMNA D2) |
| **7. Policy evaluation** | Quantitative scenario comparisons with uncertainty, for that society | cluster | — |

**Why the society comes first (DEC-11).** In Paolo's words, the learning core
is "harder and more abstract", and a basic model of society "will help
motivation". The agents' world must be defined first, including "a realistic
but optimal handling of step update", which "could be extremely slow if
implemented in a suboptimal way".

**Why this is possible.** The society and the learning core are decoupled by
the interface (conceptual model §8):
- the society sends **events** to the learning core: who heard and said how
  much, in which language, setting and register, on which day;
- the learning core returns **proficiency**: who understands and who speaks
  each language.

Until A0 exists, the **baseline learner** sits behind the interface: a simple
function from exposure to proficiency (conceptual model §8).

**What DEC-01 still requires.** No policy conclusions before the learning core
passes its gate (Phase 3). Results of Phase 2 come from the baseline learner.
They show that the mechanisms work, not what a realistic world would do.

---

## Phase 0 — Definition

1. **Settle the points that Phase 1 needs,** layer by layer, in the order of
   open points §0.1:
   - **engine** (open points §1): time unit, calendar, step and update
     frequencies; the step update and its performance budget; the stack;
     specifications before code; the package name;
   - **world** (§2): purpose and level of detail; territory and settlements;
     transport; dwellings; organisations and institutions; how the world
     changes; scaling; the world-building tools; plausible ranges and checks;
   - **population** (§3): attributes, households and kinship, demography,
     roles in organisations;
   - **activity and contact** (§4): schedules, daily mobility, groups and the
     event record, networks.

   Decided so far: DEC-07 to DEC-11.
2. **Write one specification per layer:**
   - the engine: time and the step update, with a performance budget and a
     benchmark plan;
   - the world model (`specs/world_model.md`), including the world-building
     tools;
   - the population: SM-01 demography, SM-02 partnering, SM-04 migration and
     mobility, in simple versions;
   - activity and contact: SM-05 life course and schedules, daily mobility,
     events, SM-10 networks.
3. **Collect plausible ranges** for their parameters (data inventory §2.4).

These can start at any time, because their lead time is long: the data
inventory for the learning core (data inventory §4), and the design of our
own data collection (Q-07).

**Gate 0:** the points of open points §1–§4 are settled; the specifications
of layers 1–4 are written, with plausible ranges for their parameters.

## Phase 1 — The agents' world (layers 1–4)

- **Layer 1, engine:**
  - repository skeleton: `uv` project with a package and tests, CI, run
    manifests, the parameter register;
  - random streams keyed by agent, purpose and event (SeedSequence);
  - time: the day as time unit, the simulated calendar, the weekly step,
    the update frequencies (open points §1.1);
  - the step update, with data laid out for speed and hot kernels in Numba
    where profiling demands it (open points §1.2, PROP-03);
  - snapshots of the whole state.
- **Layer 2, world:**
  - territory, settlements, districts and neighbourhoods;
  - transport and distances;
  - dwellings;
  - organisations and institutions: childcare, schools, universities, firms,
    shops and services, health, administration, justice, associations, with
    their settings and empty language slots;
  - the world-building tools: world definition, world generator, world
    checks, inspection (maps and tables).
- **Layer 3, population:**
  - people, households and kinship, generated with the world;
  - demography: SM-01, SM-02, SM-04, in simple versions;
  - roles in organisations: enrolment, hiring, leaving.
- **Layer 4, activity and contact:**
  - life course and weekly schedules (SM-05);
  - daily mobility;
  - activities, groups and the **event record**, designed for the learning
    core from the start (domains document §4.3). Events carry no language
    until Phase 2;
  - networks (SM-10).
- **Benchmarks:** 10³ agents on a laptop, then 10⁴, against the performance
  budget (open points §1.2).

**Gate 1:**
- Generated worlds pass the world checks (open points §2.9).
- Demography and time use are within plausible ranges (V29, V30 as ranges).
- Network sizes are within plausible ranges (data inventory §2.4).
- Social outputs do not depend on the order in which agents are processed,
  and a step of 1 week gives the same outputs as a step of 1 day within
  ensemble noise (validation document §4).
- The step update meets its performance budget.

## Phase 2 — Language in society

Before this phase: the points of open points §5. Develop with the baseline
learner. In order:

1. **The interface** between the society and the learning core (conceptual
   model §8), and the **baseline learner** behind it: proficiency in each
   language as a function of cumulative and recent exposure, plus an attrition
   term, with parameters from published curves (Thordardottir, Unsworth). It
   is fitted properly in Phase 3.
2. **Founding language profiles:** each language's share of speakers and its
   geography (scenario parameters).
3. **Language choice** with perceived profiles and motive-weighted choice
   (SM-11).
4. **Perceptions and motives** (SM-16) and **transmission** (SM-03), from the
   motives specification.
5. **Motivation after exclusion** (SM-14).
6. **Virtual census and language-use survey**, including the perception items
   (SM-15).
7. Benchmark 10,000 agents.

**Gate 2:**
- The behavioural unit tests of the motives model pass (motives spec §8).
- First qualitative social patterns appear with the baseline learner:
  transmission follows proficiency (V31); accommodation is asymmetric (V35).

## Phase 3 — Learning core

Before this phase: the points of open points §6, including the data
inventory, the lexicon size (Q-09) and the acceptance bands for the
single-agent targets. They can be prepared during Phases 1–2.

### 3a. Foundations

- **Lexicon v0, real pair (Catalan–Spanish):**
  - the concept table (many-to-many, function words as a separate class);
  - frequencies and contextual diversity per register;
  - spelling and IPA form distances;
  - the false-friend list.
- **Language-pair generator v0** (PROP-11): synthetic pairs from parameters.
  Its timing is open (open points §6.7).
- **Exposure model v0:**
  - scripted single-agent life histories: daily volumes by age, registers by
    age, weekly rhythm, directed vs overheard input;
  - six exposure profiles;
  - switch scenarios (one language stops at 8 or at 30).
- **Test battery v0:**
  - CDI;
  - vocabulary size;
  - simulated LexTALE-Esp, with a pseudoword model;
  - coverage;
  - cognate and non-cognate naming;
  - a provisional mapping to self-reported levels.
- **Harness:** V1–V16 and V19–V20, plus the invariance tests. Its first
  learner is the baseline learner from Phase 2, fitted here.

**Gate 3a:** the harness runs end to end with the baseline learner on the real
pair; data manifests are in place; CI passes.

### 3b. Learner A0

- **Memory-rule bake-off** (Q-08) on V1–V5, V10 and cost, with V3 as a
  gating test. Choose the rule.
- **Comprehension:** coverage, the cognate route, meaning inference.
- **Production:** competition between translation equivalents, control bias,
  language-level inhibition (review N5), reinforcement of the lemma used.
- **Age effects** on encoding and decay, and on retrieval in old age.
- **Single-agent calibration against real data:**
  - history matching on the qualitative targets;
  - simulation-based inference on the quantitative ones;
  - Sobol sensitivity analysis;
  - checks on hold-out targets.

**Gate 3b:**
- A0 is within its bands on the fit targets and on the hold-out targets.
- It beats the baseline learner on the hold-out targets.
- The memory update is exactly invariant given a fixed list of events.
- If the generator is built in this phase, a matched synthetic pair gives the
  same results as the real pair.

## Phase 4 — Generic world

- **Coupled runs:** A0 replaces the baseline learner in the society. Burn-in
  under a baseline scenario (PROP-07), then scenario runs.
- **Generic stylised facts V31–V36**, by history matching over the plausible
  parameter ranges.
- **Sweeps:**
  - over language distance, with the generator;
  - over social positions (share of speakers, geography, institutional
    support, media offer);
  - over the motive weights, including hypotheses H1–H3.
- **Exploration of policy levers**, qualitative and generic: medium of
  instruction, requirements at work, media offer.
- Emulators for the sweeps where runs are expensive.

**Gate 4:** V31–V36 are reproduced over a non-empty region of plausible
parameters, and the dependence of outcomes on the remaining parameters is
mapped and reported.

## Phase 5 — Extensions

These are independent of each other. Each has its own targets and gate:
- A1: domain semantics (semantics option S1 by default; S2 only through the gate);
- literacy (A2) and the reading and writing levels;
- ADMIN as a policy domain;
- richer motives: reactive identity, resignation (motives spec §9);
- richer media;
- a second real language pair (RQ6);
- contact and grammar (v3: F5, V21–V23);
- research tracks B0 and C0: single-agent bake-offs on the same harness
  (LMNA D3).

## Phase 6 — Specific society (Catalonia first)

- A synthetic population from the census (Q-12: options B or C become
  relevant).
- Cohort exposure histories and the **policy schedule** from 1939 onwards.
- A historical run from a start year (the old Q-03 options).
- Population calibration through emulators, with survey waves held out
  (validation document §3).

**Gate 6:** V17 and V24–V28 are within bands on the hold-out waves (LMNA D2).
If not, check the exposure model and the social layer before changing the
learner.

## Phase 7 — Policy evaluation

- Scenario design for the specific society: school hours per language,
  requirements by sector, media offer, reception of immigrants.
- Ensembles over the parameter posterior.
- Reporting with uncertainty bands, plus the sensitivity of conclusions to
  structural choices (the learner, the language-choice order, the motives
  model, scaling).

---

## Next steps together

1. Settle the points of open points §1–§4 one at a time, in the order of
   open points §0.1: time (§1.1), then the world (§2), the population (§3),
   activity and contact (§4), and the rest of the engine (§1.2–§1.5).
2. Write the specification of each layer as its points are settled, and
   collect the plausible ranges for their parameters.
3. Optional, in parallel, because the lead time is long: the data inventory
   (data inventory §4) and the design of our own data collection (Q-07).
