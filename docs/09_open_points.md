# Open points

> **Status:** living document, started 2026-11-22. Restructured the same day
> by layer (conceptual model §0.1). Updated at the end of every working
> session.
> - Every open point is listed under **the phase that needs it**. Phase 1
>   builds layers 1–4, so §1–§4 must be settled before Phase 1 starts.
> - **To resume in a new session:** read §0.1, then continue with the next
>   point.
> - Each point has its own heading, so it can be cited as "open points §2.3".
>   References follow the glossary §1; the terms of the model are defined in
>   the glossary §2 (layers and objects) and §3 (time).

---

## 0. Where we are and how we work

### 0.1 Where we are

| | |
|---|---|
| Phase | 0, Definition: preparing Phase 1, layers 1–4 (DEC-11; [`07_roadmap.md`](07_roadmap.md)) |
| First | confirm or correct the layer model (PROP-12; conceptual model §0.1) |
| Next point | §1.1, time: unit, calendar, step and update frequencies |
| Then | §2 (world), §3 (population), §4 (activity and contact), then §1.2–§1.5 (rest of the engine) |
| Last session | 2026-11-22 |

**Session log.**

| Date | What happened |
|---|---|
| 2026-11-21 | DEC-07, DEC-08 and DEC-09 decided. Motives spec drafted. |
| 2026-11-22 | Reference conventions written (glossary §1). This document created. Paolo set the birth-order requirement (§5.1). Local git repository created; no remote yet. The project folder renamed `bilangsim_v2` (DEC-10). **Society first** (DEC-11): roadmap reordered. Paolo asked for a full design of the objects of society (geography, settlements, roads, families, workplaces, schools, hospitals, justice) and of the tools to build a world, independent of the learning core. Layer model proposed (PROP-12). Terms of structure and time defined (glossary §2–§3). This document restructured by layer. |

### 0.2 How we work

1. We settle a section only when its phase is next. Within a section, we take
   one point at a time, in the order of §0.1.
2. Points marked **confirm** are proposals with no objection yet. They need a
   yes, a no or a change. Points marked **discuss** need a real choice. Points
   marked **new** are not covered by the documents yet, and need the longest
   discussion.
3. For each point, Claude states the problem, the options with what each
   trades off, and a recommendation. Paolo decides.
4. The decision goes into the document that owns the point, and into decision
   log §1 as a DEC entry with its date and reason. The point here is then
   marked **decided**, with its DEC number. It is not deleted.
5. Every new concept is defined in the glossary when it is first used.
6. Points found during the discussion are added to the section of the phase
   that needs them, with the date they were raised.
7. At the end of each session, Claude updates §0.1, and the work is
   committed.

### 0.3 Sections

| § | Layer | Needed before | Points | Output |
|---|---|---|---|---|
| 1 | 1, Engine | Phase 1 | 5 | engine specification: time and the step update |
| 2 | 2, World | Phase 1 | 9 | world-model specification (`specs/world_model.md`) |
| 3 | 3, Population | Phase 1 | 4 | population specification (SM-01, SM-02, SM-04) |
| 4 | 4, Activity and contact | Phase 1 | 4 | activity and contact specification (SM-05, SM-10) |
| 5 | 5–7, language, baseline learner, census and survey | Phase 2 | 14 (two are tasks) | revised motives spec; language-choice spec |
| 6 | 6–7, learning core and tests | Phase 3 | 11 (two are tasks) | learning-core specifications |
| 7 | — | no decision needed now | 6 | — |

---

## 1. Engine (layer 1) — before Phase 1

### 1.1 Time: unit, calendar, step and update frequencies

- **Status:** open; **confirm** PROP-04, and **discuss** the sub-questions
  below.
- **Where:** PROP-04; conceptual model §2.2; terms in the glossary §3.
- **The proposal (PROP-04):**
  - **time unit:** the day. Every event carries its day number, counted from
    day 0;
  - **step:** one week. The engine generates all the activities of the week
    and places each on its day (weekday or weekend, term or holiday);
  - **update frequencies:** demography every month; life-course transitions
    at birthdays and at the start of the academic year; institutions on the
    academic year.
- **Sub-questions the proposal leaves open:**
  - **The simulated calendar.** A year of 364 days (52 whole weeks, so steps
    and years align), or 365 days (weeks drift across years)? What is a
    month: 4 weeks, or a calendar month?
  - **Periodic checks or scheduled times.** Demography can be checked every
    month for every person ("does this person die this month?"), or each
    person's next event can be drawn as a day in advance and processed in
    the step that contains it. The second is exact and cheaper, and it does
    not depend on the step length.
  - **Events on the same day.** In which order are they applied? Learning
    reads timestamps in days, so the rule must be fixed and documented.
- **Why first:** every other layer uses these terms.

### 1.2 The step update and its performance budget

- **Status:** open; **discuss**. Raised by Paolo (2026-11-22) as crucial: a
  step update implemented in a suboptimal way could be extremely slow.
- **Where:** conceptual model §3 (the order of a simulated week); R5 and R7
  (validation document §1); invariance tests (validation document §4).
- **What it covers:**
  - how a step is processed: calendar, demography, life-course transitions,
    generating activities, forming groups, events (conceptual model §3);
  - how activities and groups are generated: per setting and in bulk, not
    agent by agent;
  - the data layout: arrays per agent, per organisation, per setting and per
    tie, rather than one object per agent;
  - random streams keyed by agent, purpose and event, so that results do not
    depend on the order of processing (CLAUDE.md, rule 5);
  - the **performance budget**, with benchmarks at 10³ and 10⁴ agents.
- **An order of magnitude.** R7 asks for 10,000 agents over 100 years "in
  hours". 100 years are about 5,200 weekly steps. If "in hours" means at most
  5 hours, one step for 10,000 agents must take under about 3.5 seconds,
  everything included: about 0.35 ms per agent per week.
- **Input from §2–§4:** each of those topics records how many objects of each
  kind exist and how often they change. These numbers set the budget. That is
  why this point is settled after §2–§4.
- **Note.** The learning core's cost comes on top, later. The event record
  (§4.3) must let it process a step's events in one batch (conceptual model
  §3, step 6).

### 1.3 The stack

- **Status:** open; **confirm**.
- **Where:** PROP-03.
- **The proposal.** One repository. Python 3.13, NumPy, and Numba for hot
  kernels (Rust only if profiling demands it). Parquet for tables, Zarr for
  snapshots, JSON run manifests. pytest and CI.
- **Linked to §1.2:** the step update decides where speed is needed.

### 1.4 Specifications before code; the parameter register

- **Status:** open; **confirm**.
- **Where:** PROP-08.

### 1.5 The package name

- **Status:** open. The repository name is decided (DEC-10).
- **Where:** Q-02.
- **Why before Phase 1:** it is needed to create the package skeleton.

---

## 2. World (layer 2) — before Phase 1

Raised by Paolo (2026-11-22): design first all the objects that make up a
society, independent of the learning core. The tools that define the world
must be well conceived, because they define the initial conditions.

### 2.1 Purpose and level of detail

- **Status:** **new**; **discuss**.
- **The question.** What must the world make possible, and how much detail
  does each object get?
- **Claude's proposal:** each object gets detail in proportion to its role
  in who meets whom, where, how often, and under which institutional norm.
  For example, few people go to a court, but its language signals which
  language the state uses, and perceived status (motives spec §3.1) is built
  from that kind of signal. So courts belong in the world, at modest detail.
- **The alternative:** realism in its own right, even where an object does
  not change who meets whom. Richer, but slower and harder to check.

### 2.2 Territory and settlements

- **Status:** **new**; includes PROP-05 (space), **discuss**.
- **Where:** PROP-05; conceptual model §2.2 and §9; domains document §6,
  question 3.
- **The questions:**
  - the territory and its subdivisions (regions, counties);
  - settlements: cities, towns, villages. How do they relate to
    municipalities (glossary §2)?
  - inside settlements: districts and neighbourhoods, and what they are for
    (neighbours, school catchment areas, local shops);
  - the size distribution (heavy-tailed, close to Zipf's law for cities;
    Gabaix, 1999); urban and rural;
  - PROP-05 proposes municipalities as nodes with distances, districts for
    large cities, and no grid. Is that enough?

### 2.3 Transport and distance

- **Status:** **new**; **discuss**.
- **The questions.** Roads, or a network of travel times between places?
  What does distance limit: commuting, the choice of school, job, hospital or
  partner, visits to relatives? Does transport change over a run?

### 2.4 Dwellings

- **Status:** **new**; **discuss**.
- **The questions.** Is there a housing stock (dwellings with a location and
  a size), or do households simply live in a district? Dwellings would limit
  where families can move and who the neighbours are.

### 2.5 Organisations and institutions

- **Status:** **new**; includes the domains of Phase 1 (domains document §0;
  §6, questions 1 and 2); **discuss**.
- **The list to settle:** childcare, schools, universities, firms (sectors,
  sizes), shops and services, health (primary care, hospitals), public
  administration, justice, associations and clubs, and media as an input.
- **For each kind:** where it is located; how many per population; its size;
  its roles (staff, users); its settings (a school has classes and a
  playground); its **language slots**, filled in Phase 2.
- **Note.** The domains document defers ADMIN and health to v2 and does not
  mention justice. As world objects they can exist from Phase 1, with their
  language role added later.
- **Also:** how many WORK sectors (the domains document proposes 5–8).

### 2.6 How the world changes

- **Status:** **new**; **discuss**.
- **The question.** Over a run of 100 years, what stays fixed and what
  evolves? Towns grow or empty, firms open and close, schools change size,
  housing is built, roads are built.

### 2.7 Population scaling

- **Status:** open; **discuss**.
- **Where:** Q-12; conceptual model §9.
- **The question.** With 10⁴ agents, each agent stands for many people.
  Settings must keep realistic sizes (a class of about 25), so their number
  shrinks, not their size. How is a world scaled down?
- **The recommendation there:** option A, a synthetic region at reduced
  scale.

### 2.8 The world-building tools

- **Status:** **new**; **discuss**.
- **The questions:**
  - the **world definition**: what it contains, and in what format;
  - the **world generator**: how it builds the world and the founding
    population, reproducibly from a seed;
  - the **world checks**: which plausible ranges a generated world must meet
    (§2.9);
  - **inspection**: maps and tables to look at a generated world;
  - later, the **importer**, which fills the same objects from the data of a
    real region (specific-society phase). Designing for it now keeps the
    object model the same in both phases.

### 2.9 Plausible ranges and checks for the world

- **Status:** **new**; **discuss**, then a Phase 0 task.
- **Where:** data inventory §2.4.
- **The questions.** Which properties of a generated world are checked, and
  against which sources: settlement sizes, household composition, sizes of
  organisations per population, commuting distances, time use, network sizes?

---

## 3. Population (layer 3) — before Phase 1

### 3.1 People's attributes

- **Status:** **new**; **discuss**.
- **The question.** What does a person carry, apart from language: age, sex,
  origin, education, occupation, traits (conceptual model §2.1)? Each
  attribute must earn its place by what it changes.

### 3.2 Households and kinship

- **Status:** open; includes PROP-07 (initial population); **discuss**.
- **Where:** PROP-07; conceptual model §2.1 and §5.
- **The questions.** Household types and how they form and split. Kinship
  in the founding population: who is whose parent, grandparent, sibling or
  cousin on day 0, when nobody has a simulated past. The burn-in (PROP-07)
  later replaces the founding families with simulated ones.

### 3.3 Demography

- **Status:** open; **discuss**; specifications SM-01, SM-02 and SM-04 to
  write.
- **Where:** conceptual model §7; legacy ideas §3.2.
- **The questions.** Births, deaths, couples, migration and residential moves:
  their rates, their plausible ranges, and how they are scheduled (§1.1,
  periodic checks or scheduled times).

### 3.4 Roles in organisations

- **Status:** **new**; **discuss**.
- **The question.** How people get and leave roles: enrolment in childcare,
  school and university; hiring and leaving jobs; registering with a doctor;
  joining associations.

---

## 4. Activity and contact (layer 4) — before Phase 1

### 4.1 Life course and weekly schedules

- **Status:** open; **discuss**; specification SM-05 to write.
- **Where:** conceptual model §7; domains document §2 and §4.5.

### 4.2 Daily mobility

- **Status:** **new**; **discuss**.
- **The question.** Who goes where, and when: home, school, work, shops,
  relatives, leisure. Linked to transport (§2.3).

### 4.3 Activities, groups and the event record

- **Status:** open; **discuss**.
- **Where:** conceptual model §3, step 5; domains document §1 and §4.3.
- **The questions.** How the people present in a setting form groups. What
  the event record holds (glossary §2): the day, the setting, the
  participants and their part (speaker, addressee, overhearer), the amount of
  speech and its register. The language is added in Phase 2.

### 4.4 Networks

- **Status:** open; **discuss**; specification SM-10 to write.
- **Where:** conceptual model §7; domains document §3.8; legacy ideas §5.
- **The questions.** Tie types (kin, partner, friend, colleague, classmate,
  neighbour, acquaintance); how ties form, strengthen and decay.

---

## 5. Before Phase 2: language in society

### 5.1 Birth order during shift

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
  - a gradual drift of the older children's relationships into mixing (§5.2);
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

### 5.2 The language of a relationship: one language or a share

- **Status:** open (raised 2026-11-22); **discuss**.
- **Where:** domains document §4.1, step 2 (relationship memory); motives spec
  §4.1.
- **The problem.** Today a relationship stores one language and can only
  switch outright, when it is renegotiated. The drift into mixing of §5.1
  needs a relationship's language to be a share that moves gradually, for
  example 70 % A and 30 % B.
- **Scope.** This would apply to every relationship (friends, colleagues), not
  only parent–child. Through the learning core, it also changes the input that
  children receive. It also affects the data layout of ties (§1.2).
- **To settle:** what moves the share (the parent's motives, the child's
  preferences, the language among siblings), how fast, and whether a
  single-language relationship stays as the special case.

### 5.3 Can the three motives be told apart?

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
  *(to check)*. A measure based on domains alone would miss that. It would
  need occupation or education among people's attributes (§3.1).

### 5.4 Status: two levels or one weight per domain

- **Status:** open; **confirm** the spec's recommendation.
- **Where:** motives spec §3.1; §9, question 3.
- **The question.** v0 has two levels: public and institutional domains weigh
  `ρ`, private ones weigh 1. The alternative is one weight per domain, about
  nine parameters.
- **The spec's recommendation:** two levels in v0. Linked to §5.3.

### 5.5 Threat at very low vitality

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
- An explicit resignation term is a separate question (§7.3).

### 5.6 Separate weights for transmission and everyday choice

- **Status:** open; **confirm** the spec's recommendation.
- **Where:** motives spec §6; §9, question 2.
- **The question.** Transmission uses the weights `β`, and everyday choice its
  own weights `α`, with the same perceptions. Only status and defence appear in
  both.
- **The spec's recommendation:** separate weights.

### 5.7 The speaker's own proficiency in everyday choice

- **Status:** open (raised 2026-11-22); **discuss**.
- **Where:** motives spec §6.
- **The problem.** Everyday choice weighs accommodation to the others, status,
  defence and the relationship's language. Nothing weighs how easily speakers
  themselves speak each language. Proficiency, the first motive of DEC-09,
  enters only indirectly, through MAXIMIN.

### 5.8 Perceived profiles

- **Status:** open; **confirm**.
- **Where:** domains document §4.2; §6, question 4.
- **The question.** People infer others' languages from cues, with noise,
  instead of knowing them. The domains document recommends this for v1,
  because accommodation depends on it.

### 5.9 Order of the language-choice steps

- **Status:** open; **confirm** or **discuss**.
- **Where:** domains document §4.1; §6, question 5; PROP-06.
- **The question.** A fixed order (institutional norm, relationship memory,
  motive-weighted choice, receptive mode, initiator, exclusion), or one
  calibrated per domain?

### 5.10 Virtual instruments

- **Status:** open; **confirm**.
- **Where:** PROP-09.
- **The proposal.** A virtual census, language-use survey and test battery,
  applied to the simulated population as to real people. Phase 2 needs the
  census and the survey; the test battery comes in Phase 3.

### 5.11 What can be calibrated while the baseline learner is in place

- **Status:** open (raised 2026-11-22); **discuss**.
- **Where:** roadmap, Phase 2; conceptual model §8.
- **The problem.** In Phase 2, every language outcome (who speaks what,
  transmission rates) depends on the baseline learner. Parameters tuned to
  those outcomes may be wrong once A0 replaces it in Phase 4.
- **Claude's proposal:** in Phase 2, calibrate only what does not depend on
  the learner (demography, schedules, networks). Explore the parameters that
  act on language outcomes, but fix them only in Phase 4, with A0.

### 5.12 The baseline learner

- **Status:** Phase 0 task, before Phase 2: write its specification.
- **Where:** conceptual model §8; review N31.
- **What:** proficiency in each language as a function of cumulative and
  recent exposure, plus an attrition term, with parameters from published
  curves (Thordardottir, Unsworth). It is fitted on the single-agent harness
  in Phase 3.

### 5.13 Qualitative bands for the stylised facts

- **Status:** Phase 0 task, before Gate 2.
- **Where:** validation document §2.4 (V31–V36).

### 5.14 Confirm the motives model

- **Status:** open, after §5.1–§5.13.
- **Where:** PROP-10.
- **What:** confirm the motives model as a whole, with the changes decided in
  this section. It then becomes a DEC entry, and the motives spec moves from
  draft v0 to v1.

---

## 6. Before Phase 3: the learning core

§6.4 and §6.10 can start at any time, because their lead time is long.

### 6.1 Approach A first, with the baseline learner as the yardstick

- **Status:** open; **confirm**. **Where:** PROP-01.

### 6.2 No vector databases; embeddings only behind the gate

- **Status:** open; **confirm**. **Where:** PROP-02.

### 6.3 Memory rule

- **Status:** open; **confirm**. **Where:** Q-08. A bake-off between four
  candidate rules, with V3 (permastore) as a gating test.

### 6.4 The data inventory

- **Status:** Phase 0 task; can start at any time. **Where:** data inventory
  §4.

### 6.5 Lexicon size for A0

- **Status:** open, after the data inventory. **Where:** Q-09.

### 6.6 Acceptance bands, and the fit and hold-out split

- **Status:** task. **Where:** validation document §2.1 and §3. For V1–V16
  and V19–V20, extracted from the published numbers before any fitting.

### 6.7 The language-pair generator

- **Status:** open; **discuss**.
- **Where:** PROP-11; conceptual model §2.3; roadmap, Phase 3a.
- **The proposal.** Generate synthetic language pairs from parameters (lexicon
  size, frequency structure, share of cognates, distribution of form
  distances), so results can be swept over linguistic distance (RQ6). The
  check: a synthetic pair matched to Catalan–Spanish must reproduce the real
  pair's results.
- **Timing, Claude's proposal (2026-11-22):** only the sweeps of Phase 4 need
  it, so build it just before them, and keep Phase 3 smaller.

### 6.8 What the generator must copy

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

### 6.9 A cheaper path

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

### 6.10 Our own data collection

- **Status:** open; can be decided at any time. **Where:** Q-07. The online
  study needs an ethics application, and its lead time is long.

### 6.11 Hosting and licence

- **Status:** open. **Where:** Q-10. Needed before anything is published, or
  before a table derived from external data is committed. The lexicon brings
  the first such tables. The local git repository exists (2026-11-22);
  nothing is published.

---

## 7. No decision needed now

Each of these has a default already written in the documents. They are
explored across ranges in the Phase 4 sweeps, or belong to later versions.

### 7.1 Compensation or conformity

- **Default:** `β_env = 0` in v0. **Where:** motives spec §4.3; §9, question
  6; hypothesis H2. Explored in Phase 4.
- **The question.** Do parents give the child the language the environment
  (school, neighbourhood) will *not* provide (compensation), or the one it
  *will* provide (conformity)?

### 7.2 Reactive identity

- **Default:** attachment fixed after childhood (`η_adult = 0`) in v0.
  **Where:** motives spec §3.3; §9, question 4. A v1 hypothesis (Phase 5,
  richer motives).
- **The question.** Does attachment to a language rise in adults who perceive
  it as threatened?

### 7.3 Resignation

- **Default:** none in v0. **Where:** motives spec §9, question 5. A v1
  hypothesis (Phase 5, richer motives). Linked to §5.5.
- **The question.** When vitality is very low, does defence give way to
  resignation?

### 7.4 Semantics option S1 or S2

- **Default:** S1, recommended. **Where:** Q-11. Needed for A1 (Phase 5).

### 7.5 Literacy

- **Default:** v2, recommended. **Where:** Q-04.

### 7.6 The contact and grammar stage

- **Default:** v3, recommended. **Where:** Q-06.

---

## References

- Gabaix, X. (1999). Zipf's law for cities: an explanation. *Quarterly Journal of Economics*, 114(3).
- Woolard, K. A. (1989). *Double Talk: Bilingualism and the Politics of Ethnicity in Catalonia*. Stanford University Press.
