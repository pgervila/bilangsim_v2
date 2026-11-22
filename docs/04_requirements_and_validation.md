# Requirements and validation

> **Status:** draft v0 (Nov 2026), for discussion. This is the **single list**
> of requirements and validation targets for the project. It consolidates:
> - R1–R8 and V1–V18 from LMNA
>   ([`background/learning_model_new_approaches.md`](background/learning_model_new_approaches.md));
> - V19–V23 from
>   [`background/modeling_solutions/essential_language_features.md`](background/modeling_solutions/essential_language_features.md);
> - new social and population targets: V24–V30 (specific society) and
>   V31–V36 (generic stylised facts), plus hypotheses H1–H3;
> - the review's corrections
>   ([`background/learning_model_docs_review.md`](background/learning_model_docs_review.md),
>   findings N3, N13–N15, X8).
>
> IDs keep their original numbers so the background documents stay readable.
> When a background document and this list disagree, this list wins.
>
> **Generic first (DEC-08).**
> - The **learning core** is tested against real data from the start (§2.1).
> - The **population** is tested first on **generic stylised facts** (§2.4).
> - Targets tied to a specific society (§2.3) wait for the specific-society
>   phase.

---

## 1. Requirements

| # | Requirement | Tested by |
|---|---|---|
| R1 | Map exposure to competence **in units that real data uses**: known-word counts, CDI checklists, test scores, comprehension coverage, census self-report levels | virtual test battery |
| R2 | Reproduce robust findings on individual learning and forgetting | V1–V16 |
| R3 | Represent interaction between the languages: competition, cognates, code-switching, dominance shifts | V14, V19, the Linck et al. fluency data |
| R4 | Represent meaning and context, so vocabulary differs by domain | V20 |
| R5 | **Same experience, same result**, whatever the bookkeeping: chunking, step length, call order, initial conditions vs live dynamics | V10 |
| R6 | **Identifiable:** few parameters, each with a source or prior, estimable from data | parameter register (§5); sensitivity analysis |
| R7 | **Scale:** 10,000 agents × 100 years in hours on a workstation; hundreds of runs for calibration | benchmarks |
| R8 | The learning core sits behind a small, stable interface, so learners can be swapped (baseline, A0, research tracks) | interface tests |
| R9 | **Social mechanisms grounded in published theory**, with parameters in plausible ranges; reproducing generic stylised facts. Calibrated on survey data in the specific-society phase. | V31–V36; later V24–V28 |
| R10 | **Population outputs in census and survey units**, through virtual instruments applied to the simulated population | V31–V36; later V17, V24–V26 |
| R11 | **Explicit, time-varying policy levers:** a policy schedule (e.g. hours of instruction per language by year and grade; requirements by sector) | scenario tests |
| R12 | **Reproducible:** a run manifest (git hash, parameters, seeds, data checksums); results as ensembles | CI checks |
| R13 | **Language-agnostic** (DEC-07). Everything specific to a language pair is data or a parameter. A synthetic pair matched to Catalan–Spanish reproduces the real pair's results. | the generator check (conceptual model §2.3) |
| R14 | **Society-agnostic** (DEC-08). No culture-specific facts in code. A language's social position (share of speakers, geography, institutional support, media) is a set of scenario parameters. | code review; scenario tests |

---

## 2. Validation targets

**Columns.**
- *Level:* single agent (S), trait distribution (T), interaction (I),
  population (P).
- *Role:* fit or hold-out. This is still to be decided (§3, step 2).
- *Band:* the acceptance band, to be fixed **before** fitting (§3, step 1).
  "TBD" everywhere for now.

### 2.1 Individual learning (single-agent harness)

| # | Finding | Source | Level | Notes |
|---|---|---|---|---|
| V1 | Spaced use beats massed use; the optimal gap grows with the retention interval | Cepeda et al. (2006, 2008) | S | |
| V2 | Forgetting has a power-law-like long tail | Wixted & Ebbesen (1991); Rubin & Wenzel (1996) | S | |
| V3 | Well-learned vocabulary reaches a "permastore" plateau | Bahrick (1984) | S | **Gating** for the memory rule. A pure power law has no plateau (review N2). |
| V4 | Adult L1 attrition is modest, even after decades | Schmid (2011); de Bot et al. (1991) | S | |
| V5 | L1 loss in childhood can be extensive | Pallier et al. (2003); Bylund (2009) | S | Wording softened after review D3 |
| V6 | Frequent words are known by more people and recognised faster; contextual diversity predicts better than frequency | SPALEX; Guasch et al. (2023); Adelman et al. (2006) | S | Contextual diversity added (review N19) |
| V7 | Comprehension needs about 95–98 % coverage | Hu & Nation (2000); Laufer & Ravenhorst-Kalovski (2010); van Zeeland & Schmitt (2013) | S | Thresholds from reading studies; listening may differ (review D2) |
| V8 | Receptive knowledge exceeds productive; the heritage profile | Polinsky & Kagan (2007) | S | |
| V9 | Plausible vocabulary growth in childhood and adulthood | Fenson et al. (1994); Wordbank; Brysbaert et al. (2016); Guasch et al. (2023) | S | Needs a lexicon large enough for adult tests (review N11) |
| V10 | Invariance to chunking, step length, call order, initial conditions vs live dynamics | — | S | **Exact** for the memory update given a fixed list of events; **statistical** for the full learner (review N3). Step length is tested separately for the coupled model (review N17). |
| V11 | Exposure share predicts vocabulary in each language; bilinguals' combined vocabulary is comparable to monolinguals' | Pearson et al. (1993); Hoff et al. (2012); Thordardottir (2011) | S | |
| V12 | Receptive vocabulary reaches monolingual levels at lower exposure than expressive | Thordardottir (2011) | S | |
| V13 | In childhood, cumulative exposure matters more than age of onset | Thordardottir (2011); Unsworth (2013) | S | |
| V14 | Cognates are named faster, more so in the non-dominant language | Costa et al. (2000) | S | |
| V15 | Incidental learning needs repeated encounters; repetition has a medium effect | Webb (2007); Uchihara et al. (2019) | S | |
| V16 | An individual's rate of forgetting is stable within one type of material | Sense et al. (2016) | T | |
| V18 | The ability to learn grammar declines after late adolescence | Hartshorne et al. (2018) | S | v3 (grammar stage) or approach C only |
| V19 | Comprehension of an unlearned closely related language rises with phonetic and lexical overlap | Gooskens (2007) | S | Needs a Catalan–Spanish listening test (to collect) |
| V20 | Bilingual children's receptive deficit is concentrated in home vocabulary, not school vocabulary | Bialystok et al. (2010) | S | Main target for domain semantics (F3) |

### 2.2 Contact and grammar (v3)

| # | Finding | Source | Level | Notes |
|---|---|---|---|---|
| V21 | Contact variants by dominance: Spanish-dominant early bilinguals accept omission and doubling of *en*/*hi*; bilingual and Spanish-dominant children acquire *en* and *ho* later | Perpiñán (2017); Soto-Corominas (2018) | S | |
| V22 | A new variant spreads through a community along an S-curve | Blythe & Croft (2012) | P | |
| V23 | Established loans are integrated and used by monolinguals; nonce borrowings are not | Poplack, Sankoff & Miller (1988) | P | |

### 2.3 Social mechanisms and population: specific-society phase

These targets need the data of one real society. Catalan sources are named
because Catalonia is the first candidate. V29 and V30 also apply to the
generic world, as **plausible ranges** rather than fits.

| # | Finding or indicator | Source | Level | Notes |
|---|---|---|---|---|
| V17 | Census knowledge of each language by age, birthplace, municipality and years of residence, over time; immigrants' L2 curves | census and *padró* language questions (series since 1986); EULP | P | Needs cohort-specific exposure histories and real demography (review N20) |
| V24 | **Language use by domain and interlocutor:** family, friends, neighbours, colleagues, shops, administration | EULP waves 2003–2023 | P | Item list to check in the questionnaires |
| V25 | **Intergenerational transmission by couple type:** language with own parents vs with own children | EULP | P | The most important social target |
| V26 | Share of linguistically mixed couples, and their home language | census or EULP *(to check)* | P | |
| V27 | Linguistic homophily of friendship networks; distribution of network sizes | EULP (language with friends); social-network surveys *(to check)* | P | |
| V28 | **Accommodation:** language used to address strangers; switching toward the interlocutor's perceived language | EULP *(item to check)*; Woolard (1989) | I | |
| V29 | Demographic structure: age pyramid, fertility, mortality, migration stocks by origin | INE, Idescat | P | Sanity check, also a fit target |
| V30 | Time use by domain and age; daily word volumes | time-use surveys; Mehl et al. (2007); LENA norms | P, S | Calibrates the exposure model (SM-12) |

V17 keeps its LMNA number. V18 appears in §2.1 because it is an
individual-level target.

### 2.4 Generic stylised facts (generic world, v1)

These patterns are reported across many bilingual societies, so a realistic
generic world should produce them without being fitted to any one society.
Their bands are qualitative or semi-quantitative: orderings, signs and rough
magnitudes.

| # | Stylised fact | Source | Level | Notes |
|---|---|---|---|---|
| V31 | Parents mostly transmit the language they speak best. Children use a language actively most often when **both** parents speak it at home; one language per parent transmits less reliably. | De Houwer (2007) | P | Motives spec: proficiency term; couple term |
| V32 | **Status gradient:** when one language dominates high-status domains (work, administration, education, media), transmission and use shift toward it over generations | Fishman (1991); status in Abrams & Strogatz (2003) | P | Status loop (motives spec §5) |
| V33 | **Three-generation shift of immigrants:** the first generation is dominant in the heritage language, the second bilingual, the third mostly monolingual in the majority language, unless the community is large and concentrated | Veltman (1983); Alba et al. (2002) | P | Needs immigration (SM-04) and transmission (SM-03) |
| V34 | **Domains retreat in order:** a receding language is lost first in public and high-status domains and survives longest at home and with older relatives | Fishman (1991) | P | Domains document §5 |
| V35 | **Accommodation asymmetry:** speakers of the lower-status language converge to the other language more than the reverse | Giles, Coupland & Coupland (1991); Woolard (1989) as a case | I | Motives spec §6 |
| V36 | **Shift, when it happens, follows an S-shaped curve** in the share of speakers over time | Abrams & Strogatz (2003) | P | |

**Hypotheses to explore, not targets.** The evidence is mixed or the
mechanism is uncertain. The generic world reports how results depend on them.

| # | Hypothesis | Where |
|---|---|---|
| H1 | Perceived threat among strongly attached speakers raises maintenance (a defence response) | motives spec §5, §9 |
| H2 | Parents compensate for the environment (negative `β_env`) rather than conform to it | motives spec §4.3 |
| H3 | Stable bilingualism needs similar languages, a small difference in status, or both | Mira & Paredes (2005); sweeps of the generator (PROP-11) |

---

## 3. Calibration protocol

1. **Fix acceptance bands before fitting.** For each target, extract the
   published numbers and turn them into bands. This is reading work in the
   definition phase ([`07_roadmap.md`](07_roadmap.md), Phase 0).
2. **Split targets into fit and hold-out before fitting** (review N13).
   - *Single-agent proposal.* Fit on V9 (CDI and prevalence), V11 and V15. Hold
     out V4–V5 (attrition), V12, V13 and V14.
   - *Generic world.* There is no fitting in the statistical sense. Explore
     the plausible parameter ranges, and keep the regions that reproduce
     V31–V36 (history matching). Report how outcomes depend on the remaining
     parameters and on H1–H3.
   - *Specific-society phase, proposal for Catalonia.* Fit on census
     1986–2011 and EULP 2003–2013. Hold out census 2021 and EULP 2018 and
     2023.
3. **Qualitative targets first, by history matching.** Targets about
   orderings (V1–V3, V8, V12–V14) rule out parameter regions (review N15).
   Quantitative targets are then fitted by simulation-based inference (neural
   posterior estimation, `sbi`) inside the region that remains.
4. **Global sensitivity analysis** (Sobol indices, SALib), on the single-agent
   harness and on the population model through emulators. Fix the parameters
   that do not matter.
5. **Uncertainty.** Draw parameters from the posterior and report ensembles
   with bands, never single runs.
6. **Baseline comparison.** Every learner must beat the baseline learner
   (conceptual model §8) on held-out targets, or it does not justify its extra
   structure (review N31).

---

## 4. Invariance tests (V10, R5)

| Test | Expectation |
|---|---|
| The same events split into different calls or batches | memory state identical (floating-point tolerance) |
| The same events processed in a different agent order | identical, because random streams are keyed to events |
| Initial conditions by spin-up vs the same history run live | identical memory state |
| Social step of 1 week vs 1 day, same schedule | population outputs equal within ensemble noise |
| Full learner (random retrieval and inference) | equal *in distribution* across chunkings |

---

## 5. Parameter register

Every parameter of every submodel is listed in one register, a table kept in
the repository and generated from code where possible. Each entry gives:
- symbol, meaning and unit;
- submodel;
- value or prior, with its source;
- fitted or fixed;
- sensitivity index, once computed;
- the targets that constrain it.

A parameter with no source and no target is a warning sign (principle P5).

## References

The references for V1–V23 are in the background documents: LMNA Appendix C,
the review, and the features document. New references:

- Abrams, D. M., & Strogatz, S. H. (2003). Modelling the dynamics of language death. *Nature*, 424, 900.
- Adelman, J. S., Brown, G. D. A., & Quesada, J. F. (2006). Contextual diversity, not word frequency, determines word-naming and lexical decision times. *Psychological Science*, 17(9).
- Alba, R., Logan, J., Lutz, A., & Stults, B. (2002). Only English by the third generation? Loss and preservation of the mother tongue among the grandchildren of contemporary immigrants. *Demography*, 39(3).
- De Houwer, A. (2007). Parental language input patterns and children's bilingual use. *Applied Psycholinguistics*, 28(3).
- Fishman, J. A. (1991). *Reversing Language Shift*. Multilingual Matters.
- Giles, H., Coupland, N., & Coupland, J. (1991). Accommodation theory. In *Contexts of Accommodation*. Cambridge University Press.
- Mira, J., & Paredes, Á. (2005). Interlinguistic similarity and language death dynamics. *Europhysics Letters*, 69(6), 1031–1034.
- Veltman, C. (1983). *Language Shift in the United States*. Mouton.
- Mehl, M. R., et al. (2007). Are women really more talkative than men? *Science*, 317(5834), 82.
- Woolard, K. A. (1989). *Double Talk*. Stanford University Press.
