# Open points

> **Status:** living document, started 2026-11-22. Re-sorted the same day by
> the phase that needs each point (DEC-11). Updated at the end of every
> working session.
> - Every open point is listed under **the phase that needs it**. Only §1
>   must be settled before Phase 1 starts.
> - **To resume in a new session:** read §0.1, then continue with the next
>   point.
> - Each point has its own heading, so it can be cited as "open points §1.2".
>   References follow the glossary §1 ([`08_glossary.md`](08_glossary.md)).

---

## 0. Where we are and how we work

### 0.1 Where we are

| | |
|---|---|
| Phase | 0, Definition: preparing Phase 1, the agents' world (DEC-11; [`07_roadmap.md`](07_roadmap.md)) |
| Next point | §1.1, time scales; then §1.2, the step update |
| Last session | 2026-11-22 |

**Session log.**

| Date | What happened |
|---|---|
| 2026-11-21 | DEC-07, DEC-08 and DEC-09 decided. Motives spec drafted. |
| 2026-11-22 | Reference conventions written (glossary §1). This document created. Paolo set the birth-order requirement (§2.1). Local git repository created; no remote yet. The project folder renamed `bilangsim_v2` (DEC-10). **Society first** (DEC-11): roadmap reordered, and this document re-sorted by the phase that needs each point. |

### 0.2 How we work

1. We settle a section only when its phase is next. Within a section, we take
   one point at a time.
2. Points marked **confirm** are proposals with no objection yet. They need a
   yes, a no or a change. Points marked **discuss** need a real choice.
3. For each point, Claude states the problem, the options with what each
   trades off, and a recommendation. Paolo decides.
4. The decision goes into the document that owns the point, and into decision
   log §1 as a DEC entry with its date and reason. The point here is then
   marked **decided**, with its DEC number. It is not deleted.
5. Points found during the discussion are added to the section of the phase
   that needs them, with the date they were raised.
6. At the end of each session, Claude updates §0.1, and the work is
   committed.

### 0.3 Sections

| § | Needed before | Points | Status |
|---|---|---|---|
| 1 | Phase 1, the agents' world | 10 (one is a task) | **now** |
| 2 | Phase 2, language in society | 14 (two are tasks) | later |
| 3 | Phase 3, the learning core | 11 (two are tasks) | later; §3.4 and §3.10 can start at any time |
| 4 | No decision needed now: explored in sweeps, or for later versions | 6 | — |

---

## 1. Before Phase 1: the agents' world

### 1.1 Time scales

- **Status:** open; **confirm**.
- **Where:** PROP-04; conceptual model §2.2.
- **The proposal.** Learning events are timestamped in days. The social
  scheduling step is one week, with events placed on actual days (weekday or
  weekend, term or holiday). Demography runs in monthly substeps.
  Institutions follow the academic year.
- **Why now:** it fixes the shape of the step update (§1.2) and of the
  invariance tests (validation document §4).

### 1.2 The step update and its performance budget

- **Status:** open; **discuss**. Raised by Paolo (2026-11-22) as crucial: a
  step update implemented in a suboptimal way could be extremely slow.
- **Where:** conceptual model §3 (the order of a simulated week); R5 and R7
  (validation document §1); invariance tests (validation document §4).
- **What it covers:**
  - how a week is processed: calendar, demography, life-course transitions,
    generating activities, forming groups, events (conceptual model §3);
  - how activities and groups are generated: per setting and in bulk, not
    agent by agent;
  - the data layout: arrays per agent, per setting and per tie, rather than
    one object per agent;
  - what runs every week, every month and every year;
  - the **event record**, designed for the learning core from the start
    (domains document §4.3): who heard and said how much, in which setting
    and register, directed or overheard, on which day;
  - random streams keyed by agent, purpose and event, so that results do not
    depend on the order of processing (CLAUDE.md, rule 5);
  - a **performance budget** that leads to R7 (10,000 agents × 100 years in
    hours on a workstation), with benchmarks at 10³ and 10⁴ agents.
- **Note.** The learning core's cost comes on top, later. The event record
  must let it process a week's events in one batch (conceptual model §3,
  step 6).
- **Output:** a specification of the step update, written before code
  (PROP-08).

### 1.3 The stack

- **Status:** open; **confirm**.
- **Where:** PROP-03.
- **The proposal.** One repository. Python 3.13, NumPy, and Numba for hot
  kernels (Rust only if profiling demands it). Parquet for tables, Zarr for
  snapshots, JSON run manifests. pytest and CI.
- **Linked to §1.2:** the step update decides where speed is needed.

### 1.4 Space

- **Status:** open; **confirm**.
- **Where:** PROP-05; domains document §6, question 3.
- **The proposal.** Municipalities as nodes with distances, districts for
  large cities, settings inside them. No grid.

### 1.5 Population scaling

- **Status:** open; **discuss**.
- **Where:** Q-12; conceptual model §9.
- **The question.** With 10⁴ agents, each agent stands for many people.
  Settings must keep realistic sizes (a class of about 25), so their number
  shrinks, not their size.
- **The recommendation there:** option A, a synthetic region at reduced
  scale, whose municipality sizes follow a realistic heavy-tailed
  distribution.

### 1.6 The domains of Phase 1, and their detail

- **Status:** open; **discuss**.
- **Where:** domains document §0; §6, questions 1 and 2.
- **The questions.** Which domains enter Phase 1? The v1 list is HOME, CARE,
  SCHOOL, UNIV, WORK, SERV, SOCIAL and PUBLIC, with MEDIA as an input and
  ADMIN in v2. And how many WORK sectors? The proposal is 5–8.

### 1.7 The initial population

- **Status:** open; **confirm**.
- **Where:** PROP-07; conceptual model §5.
- **The proposal.** A synthetic population drawn from parameterised
  distributions. Phase 1 needs only its demographic part. Founding language
  knowledge comes in Phase 2, and the burn-in in Phase 4.

### 1.8 Specifications before code; the parameter register

- **Status:** open; **confirm**.
- **Where:** PROP-08.

### 1.9 The package name

- **Status:** open. The repository name is decided (DEC-10).
- **Where:** Q-02.
- **Why now:** it is needed to create the package skeleton.

### 1.10 Plausible ranges for the Phase 1 parameters

- **Status:** Phase 0 task.
- **Where:** data inventory §2.4.
- **What:** demography, households, municipality sizes, class and workplace
  sizes, network sizes, time use by age.

---

## 2. Before Phase 2: language in society

### 2.1 Birth order during shift

- **Status:** requirement set by Paolo (2026-11-22); mechanism open;
  **discuss**.
- **Where:** motives spec §4.1; §9, question 1.
- **The requirement.** During language shift, a parent may speak the minority
  language to the older children and the majority language to the younger
  ones, and later start mixing languages with the older ones. The model must
  produce this.
- **What the spec does now.** Each parent chooses a language at every birth,
  by an independent weighted draw (a logit, motives spec §4.3). Later change
  goes only through renegotiation of the relationship.
- **Ruled out.** Deciding once, at the first child, with later children
  starting in the older child's language. Younger children would get the same
  language as the older ones.
- **What the requirement needs:**
  - a fresh choice at each birth, made with the parent's motives *at that
    moment*. By then the parent may perceive the majority language as more
    useful, and may speak it better;
  - a gradual drift of the older children's relationships into mixing (§2.2);
  - a published source for the pattern, so it can become a validation target
    (CLAUDE.md, rule 2). Still to find.
- **Claude's proposal, to discuss: some consistency within a family.** With
  independent draws, siblings differ by chance alone. A parent with
  P(A) = 0.6 at each birth addresses two children in different languages 48 %
  of the time. A consistency pull would have to be weak enough to allow the
  switch Paolo describes.
- **Milestones.** The spec recommends no re-decision at school entry, only
  renegotiation, with the child's own preferences counting from about age
  5–6. Not yet discussed.

### 2.2 The language of a relationship: one language or a share

- **Status:** open (raised 2026-11-22); **discuss**.
- **Where:** domains document §4.1, step 2 (relationship memory); motives spec
  §4.1.
- **The problem.** Today a relationship stores one language and can only
  switch outright, when it is renegotiated. The drift into mixing of §2.1
  needs a relationship's language to be a share that moves gradually, for
  example 70 % A and 30 % B.
- **Scope.** This would apply to every relationship (friends, colleagues), not
  only parent–child. Through the learning core, it also changes the input that
  children receive. It also affects the data layout of ties (§1.2).
- **To settle:** what moves the share (the parent's motives, the child's
  preferences, the language among siblings), how fast, and whether a
  single-language relationship stays as the special case.

### 2.3 Can the three motives be told apart?

- **Status:** open (raised 2026-11-22); **discuss**.
- **Where:** motives spec §3 and §7.
- **The problem.** Proficiency, perceived status and perceived vitality are all
  built from the same stream: what the person hears.
  - Proficiency follows exposure, through the learning core.
  - Perceived vitality is the share of each language in what the person
    hears.
  - Perceived status is the same share, with public events (work, school,
    administration, media) counted `ρ` times more than private ones (motives
    spec §3.1).

  Unless `ρ` is well above 1, the three move together. The model then cannot
  say which motive drove a change, which was the reason for separating them
  (motives spec §1).
- **To settle:** whether status needs a source of its own, beyond reweighting
  what a person hears.
- **One option to discuss:** status also from *who* speaks a language (their
  jobs, their education), not only from *where* it is heard. Woolard (1989)
  found that in Barcelona Catalan carried high status as the language of the
  local middle and upper classes, while Spanish dominated state institutions
  *(to check)*. A measure based on domains alone would miss that.

### 2.4 Status: two levels or one weight per domain

- **Status:** open; **confirm** the spec's recommendation.
- **Where:** motives spec §3.1; §9, question 3.
- **The question.** v0 has two levels: public and institutional domains weigh
  `ρ`, private ones weigh 1. The alternative is one weight per domain, about
  nine parameters.
- **The spec's recommendation:** two levels in v0. Linked to §2.3.

### 2.5 Threat at very low vitality

- **Status:** open (raised 2026-11-22); **discuss**.
- **Where:** motives spec §3.2; §9, question 5.
- **Now:** `threat = max(0, vit_slow − vit_fast) / vit_slow`, the decline
  relative to how it used to be.
- **The problem.** Because it is relative, threat can be large when the
  language is already rare. A fall in perceived vitality from 0.10 to 0.05
  gives the same threat (0.5) as a fall from 0.8 to 0.4. That is the opposite
  of resignation, where people stop defending a language that seems lost.
- **Options to discuss:**
  - relative decline (now);
  - absolute decline, `vit_slow − vit_fast`, which shrinks by itself as the
    language becomes rare.
- An explicit resignation term is a separate question (§4.3).

### 2.6 Separate weights for transmission and everyday choice

- **Status:** open; **confirm** the spec's recommendation.
- **Where:** motives spec §6; §9, question 2.
- **The question.** Transmission uses the weights `β`, and everyday choice its
  own weights `α`, with the same perceptions. Only status and defence appear in
  both.
- **The spec's recommendation:** separate weights.

### 2.7 The speaker's own proficiency in everyday choice

- **Status:** open (raised 2026-11-22); **discuss**.
- **Where:** motives spec §6.
- **The problem.** Everyday choice weighs accommodation to the others, status,
  defence and the relationship's language. Nothing weighs how easily speakers
  themselves speak each language. Proficiency, the first motive of DEC-09,
  enters only indirectly, through MAXIMIN.

### 2.8 Perceived profiles

- **Status:** open; **confirm**.
- **Where:** domains document §4.2; §6, question 4.
- **The question.** People infer others' languages from cues, with noise,
  instead of knowing them. The domains document recommends this for v1,
  because accommodation depends on it.

### 2.9 Order of the language-choice steps

- **Status:** open; **confirm** or **discuss**.
- **Where:** domains document §4.1; §6, question 5; PROP-06.
- **The question.** A fixed order (institutional norm, relationship memory,
  motive-weighted choice, receptive mode, initiator, exclusion), or one
  calibrated per domain?

### 2.10 Virtual instruments

- **Status:** open; **confirm**.
- **Where:** PROP-09.
- **The proposal.** A virtual census, language-use survey and test battery,
  applied to the simulated population as to real people. Phase 2 needs the
  census and the survey; the test battery comes in Phase 3.

### 2.11 What can be calibrated while the baseline learner is in place

- **Status:** open (raised 2026-11-22); **discuss**.
- **Where:** roadmap, Phase 2; conceptual model §8.
- **The problem.** In Phase 2, every language outcome (who speaks what,
  transmission rates) depends on the baseline learner. Parameters tuned to
  those outcomes may be wrong once A0 replaces it in Phase 4.
- **Claude's proposal:** in Phase 2, calibrate only what does not depend on
  the learner (demography, schedules, networks). Explore the parameters that
  act on language outcomes, but fix them only in Phase 4, with A0.

### 2.12 The baseline learner

- **Status:** Phase 0 task, before Phase 2: write its specification.
- **Where:** conceptual model §8; review N31.
- **What:** proficiency in each language as a function of cumulative and
  recent exposure, plus an attrition term, with parameters from published
  curves (Thordardottir, Unsworth). It is fitted on the single-agent harness
  in Phase 3.

### 2.13 Qualitative bands for the stylised facts

- **Status:** Phase 0 task, before Gate 2.
- **Where:** validation document §2.4 (V31–V36).

### 2.14 Confirm the motives model

- **Status:** open, after §2.1–§2.13.
- **Where:** PROP-10.
- **What:** confirm the motives model as a whole, with the changes decided in
  this section. It then becomes a DEC entry, and the motives spec moves from
  draft v0 to v1.

---

## 3. Before Phase 3: the learning core

§3.4 and §3.10 can start at any time, because their lead time is long.

### 3.1 Approach A first, with the baseline learner as the yardstick

- **Status:** open; **confirm**. **Where:** PROP-01.

### 3.2 No vector databases; embeddings only behind the gate

- **Status:** open; **confirm**. **Where:** PROP-02.

### 3.3 Memory rule

- **Status:** open; **confirm**. **Where:** Q-08. A bake-off between four
  candidate rules, with V3 (permastore) as a gating test.

### 3.4 The data inventory

- **Status:** Phase 0 task; can start at any time. **Where:** data inventory
  §4.

### 3.5 Lexicon size for A0

- **Status:** open, after the data inventory. **Where:** Q-09.

### 3.6 Acceptance bands, and the fit and hold-out split

- **Status:** task. **Where:** validation document §2.1 and §3. For V1–V16
  and V19–V20, extracted from the published numbers before any fitting.

### 3.7 The language-pair generator

- **Status:** open; **discuss**.
- **Where:** PROP-11; conceptual model §2.3; roadmap, Phase 3a.
- **The proposal.** Generate synthetic language pairs from parameters (lexicon
  size, frequency structure, share of cognates, distribution of form
  distances), so results can be swept over linguistic distance (RQ6). The
  check: a synthetic pair matched to Catalan–Spanish must reproduce the real
  pair's results.
- **Timing, Claude's proposal (2026-11-22):** only the sweeps of Phase 4 need
  it, so build it just before them, and keep Phase 3 smaller.

### 3.8 What the generator must copy

- **Status:** open (raised 2026-11-22); **discuss**.
- **Where:** PROP-11.
- **The problem.** In a real pair, how similar two translation equivalents are
  depends on the word. It varies with frequency and with register. For
  example, school and academic words may be cognates more often than everyday
  home words *(to check for Catalan–Spanish)*. Comprehension depends on how
  many of the *frequent* words are cognates. A synthetic pair that copies only
  the overall share of cognates would fail the check.
- **To settle:** which joint properties the generator must copy. At least the
  share of cognates by frequency band and by register.

### 3.9 A cheaper path

- **Status:** open (raised 2026-11-22); **discuss**.
- **Where:** PROP-11.
- **The idea.** Keep the real Catalan–Spanish lexicon (its words, frequencies
  and concept table) and vary only the form distances between translation
  equivalents, to make the pair closer or more distant. That covers the sweep
  over distance (RQ6) without generating whole lexicons. A full generator
  would still be needed for pairs whose lexicons differ in other ways, such as
  a distant second real pair (v2).
- **A limit of both paths:** they vary *lexical* distance only. Grammar is not
  in v1 (features document, F5), so neither captures grammatical distance, as
  between Basque and Spanish.

### 3.10 Our own data collection

- **Status:** open; can be decided at any time. **Where:** Q-07. The online
  study needs an ethics application, and its lead time is long.

### 3.11 Hosting and licence

- **Status:** open. **Where:** Q-10. Needed before anything is published, or
  before a table derived from external data is committed. The lexicon brings
  the first such tables. The local git repository exists (2026-11-22);
  nothing is published.

---

## 4. No decision needed now

Each of these has a default already written in the documents. They are
explored across ranges in the Phase 4 sweeps, or belong to later versions.

### 4.1 Compensation or conformity

- **Default:** `β_env = 0` in v0. **Where:** motives spec §4.3; §9, question
  6; hypothesis H2. Explored in Phase 4.
- **The question.** Do parents give the child the language the environment
  (school, neighbourhood) will *not* provide (compensation), or the one it
  *will* provide (conformity)?

### 4.2 Reactive identity

- **Default:** attachment fixed after childhood (`η_adult = 0`) in v0.
  **Where:** motives spec §3.3; §9, question 4. A v1 hypothesis (Phase 5,
  richer motives).
- **The question.** Does attachment to a language rise in adults who perceive
  it as threatened?

### 4.3 Resignation

- **Default:** none in v0. **Where:** motives spec §9, question 5. A v1
  hypothesis (Phase 5, richer motives). Linked to §2.5.
- **The question.** When vitality is very low, does defence give way to
  resignation?

### 4.4 Semantics option S1 or S2

- **Default:** S1, recommended. **Where:** Q-11. Needed for A1 (Phase 5).

### 4.5 Literacy

- **Default:** v2, recommended. **Where:** Q-04.

### 4.6 The contact and grammar stage

- **Default:** v3, recommended. **Where:** Q-06.

---

## References

- Woolard, K. A. (1989). *Double Talk: Bilingualism and the Politics of Ethnicity in Catalonia*. Stanford University Press.
