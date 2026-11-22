# Roadmap

> **Status:** draft v1 (2026-11-21), for discussion. It follows two decisions:
> - **DEC-01:** the learning model before policy;
> - **DEC-08:** a realistic generic world first, and correlation with a
>   specific society later.
>
> Each phase ends at a **gate**: an explicit check that must pass before the
> next phase starts. Hardware tiers come from LMNA §4.11.

---

## Overview

| Phase | Goal | Hardware | Gate |
|---|---|---|---|
| **0. Definition** (now) | Agree what to build and how it is judged | — | documents agreed; bands fixed; data inventory |
| **1. Foundations** | Repository, lexicon and language-pair generator, exposure model v0, test battery v0, harness, baseline learner | laptop | the harness runs end to end |
| **2. Learning core A0** | A grounded single-agent learner that passes its targets **against real data** | laptop | A0 passes its bands and beats the baseline (LMNA D1) |
| **3. Social layer v1** | Generic population, domains, networks, language choice, motives and transmission, measurement | laptop, then workstation | sanity and qualitative social patterns |
| **4. Generic world** | The coupled generic world: burn-in, generic stylised facts, sweeps over parameters, exploration of policy levers | workstation; cluster for sweeps | V31–V36 reproduced across plausible ranges |
| **5. Extensions** | Domain semantics, literacy, administration, richer motives, richer media, a second real language pair, contact and grammar; research tracks B/C | as needed | per extension (LMNA D3 for B/C) |
| **6. Specific society** | Correlation with one real society (Catalonia first): census population, cohort histories, calibration with hold-out waves | workstation and cluster | V17, V24–V28 on hold-out waves (LMNA D2) |
| **7. Policy evaluation** | Quantitative scenario comparisons with uncertainty, for that society | cluster | — |

---

## Phase 0 — Definition

1. **Review and agree** documents 01–06 and the motives specification.
   Decided so far: Q-01 (DEC-07), Q-03 (DEC-08), Q-05 (DEC-09). Still open,
   with priority: Q-02 (names), Q-08 (bake-off plan), Q-09 (lexicon size,
   after the inventory), Q-10 (licence), PROP-10 (motives model), PROP-11
   (language-pair generator).
2. **Fix acceptance bands** for the single-agent targets (V1–V16, V19–V20),
   extracting the published numbers before any fitting. Also write the
   qualitative bands for the generic stylised facts (V31–V36).
3. **Data inventory** (data inventory §4): download and profile the lexical
   and test resources; check licences.
4. **Write specifications** for the first submodels:
   - SM-12 exposure model v0 (scripted histories);
   - SM-13 learning core A0;
   - SM-15 test battery v0;
   - the baseline learner;
   - the language-pair generator.

   (SM-03 and SM-16 are already drafted in the motives specification.)
5. **Create the repository** (Q-02, Q-10) and copy this folder into it.

**Gate 0:** the documents are agreed; bands are fixed for the single-agent
targets and the stylised facts; the inventory report is written; Q-09 is
decided.

## Phase 1 — Foundations

- **Repository skeleton:**
  - `uv` project with a package and tests;
  - CI;
  - random-stream conventions (SeedSequence keyed by agent, purpose and
    event);
  - run manifests;
  - the parameter register.
- **Lexicon v0, real pair (Catalan–Spanish):**
  - the concept table (many-to-many, function words as a separate class);
  - frequencies and contextual diversity per register;
  - spelling and IPA form distances;
  - the false-friend list.
- **Language-pair generator v0** (PROP-11): synthetic pairs from parameters.
  Check it against the real pair on the single-agent harness.
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
- **Harness:** V1–V16 and V19–V20, plus the invariance tests.
- **Baseline learner:** proficiency as a fitted function of cumulative and
  recent exposure, plus attrition.
- **Online study:** design and ethics application (Q-07).

**Gate 1:** the harness runs end to end with the baseline learner, on the real
pair and on a matched synthetic pair; data manifests are in place; CI passes.

## Phase 2 — Learning core A0

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

**Gate 2:**
- A0 is within its bands on the fit targets and on the hold-out targets.
- It beats the baseline learner on the hold-out targets.
- The memory update is exactly invariant given a fixed list of events.
- A matched synthetic pair gives the same results as the real pair.

## Phase 3 — Social layer v1 (generic)

The specifications are written during Phases 1–2 (Q-13). Implementation, in
order:

1. Generic synthetic population and demography from parameterised
   distributions (SM-01, SM-02, SM-04).
2. Life course and weekly schedules (SM-05).
3. Settings by domain (SM-06 to SM-09).
4. Networks (SM-10).
5. **Perceptions and motives** (SM-16) and **transmission** (SM-03), from the
   motives specification.
6. Language choice with perceived profiles and motive-weighted choice
   (SM-11).
7. Motivation after exclusion (SM-14).
8. Virtual census and language-use survey, including the perception items
   (SM-15).

Develop and test with the baseline learner first, then switch to A0.
Benchmark 10,000 agents.

**Gate 3:**
- The behavioural unit tests of the motives model pass (motives spec §8).
- Demography and time use are within plausible ranges (V29, V30 as ranges).
- First qualitative social patterns appear: transmission follows proficiency
  (V31); accommodation is asymmetric (V35).

## Phase 4 — Generic world

- **Coupled runs:** burn-in under a baseline scenario (PROP-07), then
  scenario runs.
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

1. Review the motives specification
   ([`specs/motives_and_transmission.md`](specs/motives_and_transmission.md)),
   especially its open questions (§9).
2. Decide Q-02 and Q-10 when the repository is created.
3. Run the data inventory for the lexical and test resources. I can write the
   download and profiling scripts once the repository exists.
4. Extract the acceptance bands for V1–V16, and write the qualitative bands
   for V31–V36.
5. Draft the specifications of the exposure model v0, A0, the baseline learner
   and the language-pair generator.
