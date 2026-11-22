# Data inventory

> **Status:** draft v0 (Nov 2026), updated 2026-11-22 (world parameters in §2.4). **None of these resources has been opened or
> profiled yet.** Sizes, coverage, item lists and licences are unknown until
> the inventory task in §4. Everything marked *(to check)* is an assumption to
> verify.

---

## 1. How data is handled

- **Raw data is not committed.** Each resource gets a manifest entry: source
  URL, version or date, licence, checksum, download script, and the derived
  tables built from it.
- **Derived tables** are stored in Parquet and versioned by the checksums of
  their inputs. Run manifests record those checksums (requirement R12).
- **Licences are checked before use**, and before anything derived from a
  resource is published.

---

## 2. Existing resources

### 2.1 Lexicon and language structure (learning core, features F1–F4)

| Resource | Content | Used for | Priority | Licence and access |
|---|---|---|---|---|
| **SUBTLEX-CAT** (Boada et al., 2020) | Catalan subtitle word frequencies and contextual diversity, ~278 M words | adult conversational register; frequency and contextual diversity (V6) | v0 | *(to check redistribution)* |
| **SUBTLEX-ESP** (Cuetos et al., 2011) | Spanish subtitle frequencies | as above | v0 | *(to check; is contextual diversity included?)* |
| **CHILDES** Catalan and Spanish corpora, incl. Serra/Solé | child-directed and child speech, ages ~1–4 | child-directed register; infant input | v0 | TalkBank ground rules *(to check)*; **size in tokens to measure** (review N26) |
| spaCy / Stanza pipelines | lemmatisation and part of speech for Catalan and Spanish | turning word forms into lemmas | v0 | open source |
| **Apertium spa–cat** bilingual dictionary | translation equivalents | the concept table | v0 | GPL *(to check terms for derived data)*; **share of one-to-one pairs to measure** (review N9) |
| espeak-ng | IPA transcriptions | phonological form distance (F2) | v0 | open source |
| rapidfuzz | edit distances | orthographic form distance (F2) | v0 | open source |
| **MCR wordnets** (Catalan, Spanish; WordNet 3.0 Inter-Lingual Index) | synsets, relations, domain labels | sense-level concepts; domain labels (F3) | v1 | CC BY 3.0 for non-English data; **coverage of the lemma list to measure** |
| fastText aligned vectors (ca, es) | embeddings | optional; only if they pass the gate in `embeddings_and_vector_databases.md` | gated | CC BY-SA 3.0 |
| Register corpora: school textbooks, classroom transcripts, work by sector | per-setting frequencies | domain vocabulary (F3) | v1 | **availability unknown** *(to search)* |

### 2.2 Tests and norms (virtual test battery)

| Resource | Content | Used for | Priority | Licence and access |
|---|---|---|---|---|
| **Wordbank** (European Spanish CDI) | children's words understood and produced, by age | V9, V11 | v0 | *(to check)* |
| Catalan CDI adaptation | the same, in Catalan | V9, V11 | v0 | **data access to check** |
| **Guasch et al. (2023)** prevalence norms | 40,777 Catalan words, >200,000 participants, by age | adult vocabulary (V6, V9) | v0 | *(to check)* |
| **SPALEX** (Aguasvivas et al., 2018) | Spanish lexical decision for 45,389 words, ~170,000 participants, with response times | V6, V9 | v0 | *(to check)* |
| Spanish age-of-acquisition norms (Alonso et al., 2015) | 7,039 words | AoA checks | v1 | *(to check)*; no Catalan equivalent found |
| **LexTALE-Esp** (Izura et al., 2014) | lexical-decision test items | adult proficiency; dominance (Ferré & Brysbaert, 2017) | v0 | items published; **pseudoword response model needed** (review N12) |
| Picture-naming items with cognates and non-cognates | naming latency, cognate effect | V14 | v1 | *(to build from published item sets)* |
| Published results for the validation targets V1–V23 | numbers for the acceptance bands | §3 of the validation document | Phase 0 | from the papers |

### 2.3 Exposure (exposure model, SM-12)

| Resource | Content | Used for | Priority |
|---|---|---|---|
| Mehl et al. (2007) | words spoken per day by adults | adult volumes (V30) | v0 |
| LENA norms (Gilkerson et al., 2017) | adult words heard by children per day | child volumes | v0 |
| Weisleder & Fernald (2013) | directed vs overheard speech and vocabulary | weights for directed vs overheard input | v0 |
| **Time-use surveys** (INE *Encuesta de Empleo del Tiempo*; a Catalan edition *(to check)*) | time per activity by age and sex | weekly schedules (SM-05, V30) | v1 |

### 2.4 Plausible ranges for the generic world (v1)

The generic world (DEC-08) needs **ranges**, not fits. Each social parameter
gets a plausible interval from the literature or from cross-national
statistics, rather than the value for one place and year.

| Parameter group | Where the ranges come from | Used for |
|---|---|---|
| Mortality, fertility, age structure, household types | life tables and demographic statistics of several countries (e.g. Eurostat) *(sources to choose)* | SM-01, SM-02; V29 |
| Municipality size distribution | heavy-tailed town sizes (Zipf's law for cities; Gabaix, 1999); national municipality lists | space and scaling (conceptual model §9) |
| Class sizes, school stages, enrolment by age | education statistics (e.g. OECD *Education at a Glance*) *(to check)* | SM-06 |
| Workplace sizes, sectors | business and labour statistics *(to choose)* | SM-07 |
| Transport and commuting distances | commuting statistics of several countries; models of commuting flows *(sources to search)* | world: transport (open points §2.3); daily mobility (open points §4.2) |
| Dwellings and household sizes | housing and census statistics of several countries *(sources to choose)* | world: dwellings (open points §2.4); households (open points §3.2) |
| Organisations per population: childcare, health, administration, justice, shops, associations | public-service and business statistics *(sources to choose)* | world: organisations (open points §2.5) |
| Network sizes, homophily | the social-network literature *(to search)* | SM-10 |
| Time per domain by age | time-use surveys (e.g. harmonised European time-use surveys) *(to check)* | SM-05; V30 |
| Words per day | Mehl et al. (2007); LENA norms | SM-12; V30 |
| Immigration rates; immigrant transmission | migration statistics; studies of immigrant language shift (Veltman, 1983; Alba et al., 2002) | SM-04; V33 |
| Weights of the motives | the transmission and attitudes literature (motives spec §2); explored, not fixed | SM-03, SM-16 |

### 2.5 Society data for the specific-society phase (later)

Catalonia is the first candidate society.

| Resource | Content | Used for | Phase | Access |
|---|---|---|---|---|
| **Census and *padró* language questions** (Idescat) | knowledge of Catalan (understands, speaks, reads, writes) by age, birthplace, municipality; series since 1986 *(years to confirm)* | V17; initial population | specific society | tables public; microdata *(to check)* |
| **EULP** (*Enquesta d'usos lingüístics de la població*; 2003, 2008, 2013, 2018, 2023) | language use by interlocutor and domain; first and habitual language; transmission; attitudes and identification; population aged 15+ | V24–V28; calibration of language choice, transmission and motives | specific society. *Exception:* listing its questionnaire items early helps design the virtual survey (SM-15). | reports public; **microdata access to check** |
| INE / Idescat demography | life tables, fertility, births, deaths | SM-01, V29 | specific society | public |
| Migration statistics (INE residential variations; *padró* by birthplace) | inflows and stocks by origin | SM-04, V17, V29 | specific society | public |
| Municipalities (Idescat) | population, coordinates, districts | space and scaling | specific society | public |
| Labour-force survey (EPA; Idescat labour data) | employment by sector and area | SM-07 | specific society | public tables |
| Education statistics and **curriculum regulations** | enrolment by age; hours of instruction per language; history of school language regimes | SM-06; policy schedule (R11) | specific society | public |
| **Language-policy history** | 1939–75 exclusion of Catalan; 1983 normalisation law; 1998 language-policy law; changes in school regimes | cohort exposure histories (review N20); policy schedule | specific society | literature, legal texts |
| Media audiences by language | consumption per language, age, medium | SM-09, V24 | specific society | sources *(to check)*: audience barometers, regulator reports |
| Social-network surveys | network size and composition | V27 | specific society | *(to search)* |

### 2.6 Contact and grammar (v3)

| Resource | Content | Used for |
|---|---|---|
| Perpiñán (2017); Soto-Corominas (2018) | clitic acceptability and production by dominance; child acquisition | V21 |
| Spoken Catalan corpora with sociolinguistic metadata | rates of contact variants by age and dominance | V21–V23 *(to search)* |
| Lists of Castilianisms; normative references | variant inventory | F5 |

---

## 3. Data we can collect ourselves

From LMNA §3.8, extended. All of it needs GDPR compliance, informed consent
and ethics approval.

| Study | Measures | Targets it serves | Lead time |
|---|---|---|---|
| **Online bilingual vocabulary study** | LexTALE-style tests in Catalan and Spanish; language history (LEAP-Q or Bilingual Language Profile). Extensions: a listening test of the unlearned language (V19) and a short acceptability module on contact variables (V21). | V6, V9, V11, V19, V21; the most informative single dataset for calibration | long: start early |
| Experience sampling | interlocutor, place, language, duration | exposure model; V24, V30 | medium |
| Daylong audio in bilingual families | children's input per language (automatic language identification) | infant exposure; directed vs overheard | long |
| Longitudinal follow-up of people who move | attrition | V4, V5 | very long |
| Spontaneous Catalan–Spanish conversation corpus | code-switching and borrowing rates | F4, F5 | medium |

---

## 4. First data task: the inventory

Before the learning core is designed in detail, download and **profile** each
v0 resource. Report:

1. **SUBTLEX-CAT/ESP.** How many word forms and lemmas, and what lemmatisation
   loses. Is contextual diversity available for Spanish?
2. **CHILDES ca/es.** Tokens by age band and register; speakers; how much is
   directed to children.
3. **Apertium spa–cat.** Pairs among the top 5k, 10k, 20k and 30k lemmas:
   share one-to-one, many-to-many, unmatched.
4. **MCR.** Coverage of the lemma list by synsets and domain labels.
5. **Tests.** Access to Wordbank (European Spanish) and the Catalan CDI;
   LexTALE-Esp items; the Guasch and SPALEX files.
6. **EULP questionnaire items** by wave (interlocutors, domains,
   transmission, strangers, attitudes, identification). They are needed early
   only as a model for the virtual survey. Microdata waits for the
   specific-society phase.
7. **Licences**, for each resource.

The answers decide the lexicon size (Q-09), the feasible tests, and the fit
and hold-out split for the learning core. Census tables and EULP microdata
are profiled later, in the specific-society phase.

## References

Full references for the lexical and test resources are in LMNA Appendix C
([`background/learning_model_new_approaches.md`](background/learning_model_new_approaches.md)),
and for contact studies in the features document. Additional:

- Alba, R., Logan, J., Lutz, A., & Stults, B. (2002). Only English by the third generation? *Demography*, 39(3).
- Gabaix, X. (1999). Zipf's law for cities: an explanation. *Quarterly Journal of Economics*, 114(3).
- Veltman, C. (1983). *Language Shift in the United States*. Mouton.
- Weisleder, A., & Fernald, A. (2013). Talking to children matters. *Psychological Science*, 24(11).
