# Open points

> **Status:** living document, started 2026-11-22. Updated at the end of every
> working session.
> - It lists every open point of Phase 0, grouped by area of modelling, in the
>   order we settle them.
> - **To resume in a new session:** read §0.1, then continue with the next
>   point.
> - Each point has its own heading, so it can be cited as "open points §1.1".
>   References follow the glossary §1 ([`08_glossary.md`](08_glossary.md)).

---

## 0. Where we are and how we work

### 0.1 Where we are

| | |
|---|---|
| Phase | 0, Definition ([`07_roadmap.md`](07_roadmap.md)) |
| Current area | §1, Family and transmission |
| Next point | §1.1, birth order during shift |
| Last session | 2026-11-22 |

**Session log.**

| Date | What happened |
|---|---|
| 2026-11-21 | DEC-07, DEC-08 and DEC-09 decided. Motives spec drafted. |
| 2026-11-22 | Reference conventions written (glossary §1). This document created. Paolo set the birth-order requirement (§1.1). Local git repository created; no remote yet. The project folder renamed `bilangsim_v2` (DEC-10). |

### 0.2 How we work

1. We take the areas in the order of §0.3, and their points one at a time.
2. For each point, Claude states the problem, the options with what each
   trades off, and a recommendation. Paolo decides.
3. The decision goes into the document that owns the point, and into decision
   log §1 as a DEC entry with its date and reason. The point here is then
   marked **decided**, with its DEC number. It is not deleted.
4. Points found during the discussion are added to their area, with the date
   they were raised.
5. At the end of each area, Claude lists the changes by file and updates §0.1,
   and the work is committed.

### 0.3 Areas, in order

| § | Area | Points | Status |
|---|---|---|---|
| 1 | Family and transmission (SM-03) | 3 | in progress |
| 2 | Perceptions and motives (SM-16) | 4 | open |
| 3 | Language choice (SM-11), then the motives model as a whole (PROP-10) | 5 | open |
| 4 | Language pairs (PROP-11) | 5 | open |
| 5 | Learning core (SM-13) | 6 | open |
| 6 | Society structure | 6 | open |
| 7 | Measurement and population targets (SM-15) | 2 | open |
| 8 | Project and data | 7 | open |

**Why this order.** On 2026-11-22 Paolo asked to start with the open questions
of the motives spec, then PROP-10, then PROP-11. Areas 1–3 cover the motives
spec and end with PROP-10. Area 4 is PROP-11. The learning core comes next,
because Phase 1 needs it first.

---

## 1. Family and transmission (SM-03)

### 1.1 Birth order during shift

- **Status:** requirement set by Paolo (2026-11-22); mechanism open.
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
  - a gradual drift of the older children's relationships into mixing (§1.2);
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

### 1.2 The language of a relationship: one language or a share

- **Status:** open (raised 2026-11-22).
- **Where:** domains document §4.1, step 2 (relationship memory); motives spec
  §4.1.
- **The problem.** Today a relationship stores one language and can only
  switch outright, when it is renegotiated. The drift into mixing of §1.1
  needs a relationship's language to be a share that moves gradually, for
  example 70 % A and 30 % B.
- **Scope.** This would apply to every relationship (friends, colleagues), not
  only parent–child. Through the learning core, it also changes the input that
  children receive.
- **To settle:** what moves the share (the parent's motives, the child's
  preferences, the language among siblings), how fast, and whether a
  single-language relationship stays as the special case.

### 1.3 Compensation or conformity

- **Status:** open.
- **Where:** motives spec §4.3; §9, question 6; hypothesis H2 (validation
  document §2.4).
- **The question.** Do parents give the child the language the environment
  (school, neighbourhood) will *not* provide (compensation), or the one it
  *will* provide (conformity)? In the transmission choice this is the sign of
  `β_env`, set to 0 in v0.
- **The spec's recommendation:** explore both signs in the generic world.

---

## 2. Perceptions and motives (SM-16)

### 2.1 Can the three motives be told apart?

- **Status:** open (raised 2026-11-22).
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

### 2.2 Status: two levels or one weight per domain

- **Status:** open.
- **Where:** motives spec §3.1; §9, question 3.
- **The question.** v0 has two levels: public and institutional domains weigh
  `ρ`, private ones weigh 1. The alternative is one weight per domain, about
  nine parameters.
- **The spec's recommendation:** two levels in v0. Linked to §2.1.

### 2.3 Threat at very low vitality, and resignation

- **Status:** open; the first part raised 2026-11-22.
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
    language becomes rare;
  - an explicit resignation term at low vitality.
- **The spec's recommendation on resignation:** a v1 hypothesis, not in v0.

### 2.4 Reactive identity

- **Status:** open.
- **Where:** motives spec §3.3; §9, question 4.
- **The question.** Does attachment to a language rise in adults who perceive
  it as threatened? Now attachment forms in childhood and stays fixed
  afterwards (`η_adult = 0`).
- **The spec's recommendation:** not in v0; a v1 hypothesis.

---

## 3. Language choice (SM-11), then the motives model as a whole

### 3.1 Separate weights for transmission and everyday choice

- **Status:** open.
- **Where:** motives spec §6; §9, question 2.
- **The question.** Transmission uses the weights `β`, and everyday choice its
  own weights `α`, with the same perceptions. Only status and defence appear in
  both.
- **The spec's recommendation:** separate weights.

### 3.2 The speaker's own proficiency in everyday choice

- **Status:** open (raised 2026-11-22).
- **Where:** motives spec §6.
- **The problem.** Everyday choice weighs accommodation to the others, status,
  defence and the relationship's language. Nothing weighs how easily speakers
  themselves speak each language. Proficiency, the first motive of DEC-09,
  enters only indirectly, through MAXIMIN.

### 3.3 Perceived profiles in v1

- **Status:** open.
- **Where:** domains document §4.2; §6, question 4.
- **The question.** People infer others' languages from cues, with noise,
  instead of knowing them. The domains document recommends this for v1,
  because accommodation depends on it.

### 3.4 Order of the language-choice steps

- **Status:** open.
- **Where:** domains document §4.1; §6, question 5; PROP-06.
- **The question.** A fixed order (institutional norm, relationship memory,
  motive-weighted choice, receptive mode, initiator, exclusion), or one
  calibrated per domain?

### 3.5 Confirm the motives model

- **Status:** open, after §1–§3.4.
- **Where:** PROP-10.
- **What:** confirm the motives model as a whole, with the changes decided in
  §1–§3. It then becomes a DEC entry, and the motives spec moves from draft v0
  to v1.

---

## 4. Language pairs

### 4.1 The language-pair generator

- **Status:** open.
- **Where:** PROP-11; conceptual model §2.3.
- **The proposal.** Generate synthetic language pairs from parameters (lexicon
  size, frequency structure, share of cognates, distribution of form
  distances), so results can be swept over linguistic distance (RQ6). The
  check: a synthetic pair matched to Catalan–Spanish must reproduce the real
  pair's results.

### 4.2 What the generator must copy

- **Status:** open (raised 2026-11-22).
- **Where:** PROP-11.
- **The problem.** In a real pair, how similar two translation equivalents are
  depends on the word. It varies with frequency and with register. For
  example, school and academic words may be cognates more often than everyday
  home words *(to check for Catalan–Spanish)*. Comprehension depends on how
  many of the *frequent* words are cognates. A synthetic pair that copies only
  the overall share of cognates would fail the check.
- **To settle:** which joint properties the generator must copy. At least the
  share of cognates by frequency band and by register.

### 4.3 A cheaper path

- **Status:** open (raised 2026-11-22).
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

### 4.4 Lexicon size for A0

- **Status:** open, after the data inventory. **Where:** Q-09.

### 4.5 The contact and grammar stage as v3

- **Status:** open. **Where:** Q-06.

---

## 5. Learning core (SM-13)

### 5.1 Approach A first, with the baseline learner as the yardstick

- **Status:** open. **Where:** PROP-01.

### 5.2 No vector databases; embeddings only behind the gate

- **Status:** open. **Where:** PROP-02.

### 5.3 Memory rule

- **Status:** open. **Where:** Q-08. A bake-off between four candidate rules,
  with V3 (permastore) as a gating test.

### 5.4 Semantics option S1 or S2

- **Status:** open. **Where:** Q-11.

### 5.5 Literacy in v1 or v2

- **Status:** open. **Where:** Q-04.

### 5.6 Acceptance bands, and the fit and hold-out split

- **Status:** Phase 0 task. **Where:** validation document §2.1 and §3. For
  V1–V16 and V19–V20, extracted from the published numbers before any
  fitting.

---

## 6. Society structure

### 6.1 Time

- **Status:** open. **Where:** PROP-04. Days for learning events, a weekly
  social step, monthly demography.

### 6.2 Space

- **Status:** open. **Where:** PROP-05; domains document §6, question 3.
  Municipalities as nodes, with districts for large cities, and no grid.

### 6.3 Population scaling

- **Status:** open. **Where:** Q-12.

### 6.4 Initial conditions by spin-up and burn-in

- **Status:** open. **Where:** PROP-07.

### 6.5 The list of domains for v1

- **Status:** open. **Where:** domains document §6, question 1.

### 6.6 The number of WORK sectors

- **Status:** open. **Where:** domains document §6, question 2.

---

## 7. Measurement and population targets (SM-15)

### 7.1 Virtual instruments

- **Status:** open. **Where:** PROP-09. A virtual census, language-use survey
  and test battery.

### 7.2 Qualitative bands for the stylised facts

- **Status:** Phase 0 task. **Where:** validation document §2.4 (V31–V36).

---

## 8. Project and data

### 8.1 One repository, and the stack

- **Status:** open. **Where:** PROP-03.

### 8.2 A specification before code; the parameter register

- **Status:** open. **Where:** PROP-08.

### 8.3 Project and package names

- **Status:** partly decided: the repository is `bilangsim_v2` (DEC-10, 2026-11-22). The package name is still open. **Where:** Q-02.

### 8.4 Hosting and licence

- **Status:** open. **Where:** Q-10. The local git repository exists
  (2026-11-22). Nothing is published.

### 8.5 Our own data collection

- **Status:** open. **Where:** Q-07.

### 8.6 When to build the social layer

- **Status:** open. **Where:** Q-13.

### 8.7 The data inventory

- **Status:** Phase 0 task. **Where:** data inventory §4.

---

## References

- Woolard, K. A. (1989). *Double Talk: Bilingualism and the Politics of Ethnicity in Catalonia*. Stanford University Press.
