# Vision and scope

> **Status:** draft v0 (Nov 2026), for discussion. Items marked **Q-xx** are
> open questions, listed with options and recommendations in
> [`06_decisions.md`](06_decisions.md).

---

## 1. Purpose

Build an agent-based model of a bilingual society that answers one question:
**when, how fast and why does a minority language survive, shift or erode, and
what changes that?**

The model simulates individuals who are born, grow up, form families, go to
school, work, make friends, move and die. They talk to each other in the
settings of everyday life. What they hear and say decides what they learn and
forget of each language. What they know decides which language they use with
whom, which language they pass on to their children, and which opportunities
they have. Shift or survival of the minority language emerges from this loop.

The guiding question of the sociology of language applies to every mechanism:
**"Who speaks what language to whom, and when?"** (Fishman, 1965).

## 2. Research questions

| # | Question | First version? |
|---|---|---|
| RQ1 | Under which demographic, social and policy conditions does a minority language keep or lose speakers across generations? | v1 |
| RQ2 | How do parents decide which language to pass on, depending on their own proficiency, the couple's languages and the environment? What aggregate transmission rates result? | v1 |
| RQ3 | How does use evolve domain by domain (home, school, work, services, administration, friends, media)? In which order does a language retreat from domains, and why? | v1 |
| RQ4 | What do policies achieve: medium of instruction, language requirements at work and in public services, media offer, adult classes, reception of immigrants? At the level of individuals and of the population, with uncertainty. | v1 (school, work); v2 (others) |
| RQ5 | How does the minority language itself change under contact: loans, calques, grammatical convergence? | v2+ |
| RQ6 | How much do the answers depend on **how close the two languages are** and on **their social positions** (status, institutional support, share of speakers)? Explored by sweeping language-pair parameters (DEC-07). | v1 (sweeps of parameters); v2 (a second real pair, e.g. Basque–Spanish) |

## 3. What makes this model different

1. **Individual learning grounded in cognitive science and testable.** Agents
   know real words of real languages. Their learning follows established
   models of memory and of the bilingual lexicon. Single agents take the same
   tests humans take (child vocabulary checklists, vocabulary tests, lexical
   decision).
2. **General first, specific later** (DEC-08).
   - The social mechanisms (language choice, transmission, networks) are
     grounded in published theory.
   - Their parameters lie in plausible ranges, and they are tested on
     **generic stylised facts** of bilingual societies.
   - Calibration to the survey data of one specific society (e.g. Catalonia's
     census and EULP) is a later, separate phase.
   - Language pairs and their social positions are parameters (DEC-07), so
     results can be compared across kinds of societies.
3. **Outputs in the units of real data.** The model is surveyed with the same
   instruments as a real population: a virtual census, a virtual language-use
   survey and a virtual test battery. Simulated and real results can then be
   compared directly, once a specific society is targeted.
4. **Uncertainty is reported.** Results come as ensembles with uncertainty
   bands, from calibrated parameter distributions, never from single runs.

## 4. Principles

These come from the project's history and from Paolo's stated requirements
(Nov 2026).

| # | Principle | Consequence |
|---|---|---|
| P1 | **Testable against measurable data.** A mechanism that cannot be tested is not trusted. | Every submodel names its validation targets ([`04_requirements_and_validation.md`](04_requirements_and_validation.md)) |
| P2 | **Start simple, but on a scientific basis.** The first version of each submodel is minimal, and each is based on a published model. | Small first builds (e.g. learning core A0) with literature references |
| P3 | **Specified before emergent.** Mechanisms whose structure we write down come first. Emergent approaches (self-organising maps, neural agents) are research tracks that must beat them on held-out targets. | B and C stay research tracks |
| P4 | **Same experience, same result.** Time is measured in days, every event is timestamped, and results do not depend on bookkeeping. | Invariance tests |
| P5 | **Identifiable.** Few parameters, each with a source or a prior, each estimable from data. | A parameter register |
| P6 | **Uncertainty always.** Ensembles and calibrated parameter distributions. | Calibration pipeline |
| P7 | **Reproducible.** Seeded random streams, run manifests, checksums for data. | Engineering conventions |
| P8 | **No legacy code.** Keep the legacy *ideas* ([`background/modeling_solutions/legacy_best_ideas.md`](background/modeling_solutions/legacy_best_ideas.md)) and rebuild them. Validate against data, not against legacy output. | Fresh repository |
| P9 | **Scale progressively.** Laptop first; workstation for 10,000 agents; a cluster for ensembles. | Performance budgets per phase |
| P10 | **Learning model before policy.** Policy conclusions are only as good as the learning core. | Roadmap order ([`07_roadmap.md`](07_roadmap.md)) |
| P11 | **A realistic generic world first.** Realistic in structure, not tied to a country, period or calendar years. Correlation with a specific society comes later (DEC-08). | Generic stylised facts as population targets; no culture-specific constants |
| P12 | **General through parameters.** Everything specific to a language pair or to a society is data or a parameter, never hard-coded (DEC-07). | Neutral labels A and B in the social layer; a synthetic language-pair generator (PROP-11) |

## 5. Scope

### 5.1 First version (v1)

- **World:** a **realistic generic society** (DEC-08):
  - a synthetic region whose municipality sizes, demography, households,
    institutions, schedules and networks are realistic in structure, with
    parameters in plausible ranges;
  - two languages, **A** and **B**, whose social positions (share of
    speakers, geography, institutional support, media offer) are scenario
    parameters.
- **Reference language pair:** Catalan and Spanish, for the real lexicon and
  the tests of the learning core against data (DEC-07). Synthetic pairs from
  the language-pair generator cover other distances (PROP-11).
- **Language:** spoken language at the level of the lexicon:
  - a real lexicon with frequencies;
  - form overlap between the two languages (cognates);
  - words used in each setting;
  - comprehension and production, competition, code-switching (features F1–F4).
- **Society:** the domains of [`02_society_domains.md`](02_society_domains.md):
  home and family, childcare, school, university, work, services, friends and
  leisure, neighbourhood, and media as exogenous input. Plus demography,
  migration and mobility.
- **Mechanisms:**
  - language choice (MAXIMIN and accommodation, with memory of the language
    used in each relationship);
  - intergenerational transmission driven by **motives**: proficiency,
    perceived status, defence against assimilation
    ([`specs/motives_and_transmission.md`](specs/motives_and_transmission.md),
    DEC-09);
  - learning and forgetting;
  - motivated learning after exclusion.
- **Outputs:**
  - census-like knowledge categories (understands, speaks);
  - EULP-like use by domain and interlocutor;
  - transmission rates;
  - exposure per language.
- **Policies:** medium of instruction (hours per language per grade) and
  language requirements at work.

### 5.2 Later versions

| Version | Adds |
|---|---|
| v2 | literacy (reads and writes, for the census); public administration as a policy domain; adult language classes; richer motives (reactive identity, resignation; motives spec §9); richer media; a second real language pair (RQ6) |
| v3 | contact-induced change: lexical variants and grammatical variables (feature F5, RQ5) |
| **Specific-society phase** | correlation with a real society (Catalonia first): synthetic population from its census; histories specific to each birth cohort; its policy history; calibration on census and EULP, with hold-out survey waves |
| research tracks | developmental connectionist lexicon (B); neural agents (C) |

### 5.3 Out of scope

- Phonology and accent, beyond their effect on intelligibility.
- An endogenous economy.
- Coining genuinely new words (only approach C could).
- Real-time forecasting for individuals.

## 6. Success criteria for v1

1. **Single agents.** The learning core passes the single-agent validation
   targets within acceptance bands fixed before fitting.
2. **Population, generic world.** The generic world reproduces the generic
   stylised facts of bilingual societies (V31–V36), for example:
   - parents mostly transmit their strongest language;
   - immigrant families shift over three generations;
   - a receding language retreats from public domains first and survives
     longest at home;
   - speakers of the lower-status language accommodate more.

   It does so across the plausible parameter ranges, and it shows the range of
   outcomes (stable bilingualism, shift, recovery) that real societies show.
3. **Policy levers behave plausibly** in sensitivity analyses, and their
   uncertainty is quantified.
4. **Performance.** 10,000 agents over 100 years run in hours on a
   workstation, so ensembles of hundreds of runs are feasible.
5. **Documentation.** Every parameter is documented with its source or prior.
   The model is described in the ODD protocol
   ([`03_conceptual_model.md`](03_conceptual_model.md)).

**Later, in the specific-society phase:** a historical run of one real
society reproduces its census and survey data, and predicts held-out later
waves within bands.

## References

- Fishman, J. A. (1965). Who speaks what language to whom and when? *La Linguistique*, 1(2), 67–88.
- Further references are in the background documents and in the living documents that use them.
