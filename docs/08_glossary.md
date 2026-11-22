# Glossary

> **Status:** living document, updated 2026-11-22.
> - §1 explains how the documents refer to each other, to literature and to
>   code.
> - §2 is the shared vocabulary. Keep entries short. Add a term when it first
>   appears in a document.

---

## 1. How to read references

### 1.1 Sections

| Written | Means |
|---|---|
| `§4.1` on its own | section 4.1 of the **same** document |
| `motives spec §6` | section 6 of **another** document, named by its short name (§1.2) |
| `§9, question 1` | item 1 of a numbered list inside section 9. It is never written `§9.1` unless the document has a heading 9.1. |
| *(to check)* | a fact not yet verified |

### 1.2 Short names of the documents

| Short name | File |
|---|---|
| vision document | [`01_vision_and_scope.md`](01_vision_and_scope.md) |
| domains document | [`02_society_domains.md`](02_society_domains.md) |
| conceptual model | [`03_conceptual_model.md`](03_conceptual_model.md) |
| validation document | [`04_requirements_and_validation.md`](04_requirements_and_validation.md) |
| data inventory | [`05_data_inventory.md`](05_data_inventory.md) |
| decision log | [`06_decisions.md`](06_decisions.md) |
| roadmap | [`07_roadmap.md`](07_roadmap.md) |
| glossary | this document |
| open points | [`09_open_points.md`](09_open_points.md) |
| motives spec | [`specs/motives_and_transmission.md`](specs/motives_and_transmission.md) |
| LMNA | [`background/learning_model_new_approaches.md`](background/learning_model_new_approaches.md) (frozen) |
| MMA | [`background/memory_model_analysis.md`](background/memory_model_analysis.md) (frozen) |
| the review | [`background/learning_model_docs_review.md`](background/learning_model_docs_review.md) (frozen) |
| legacy analysis | [`background/legacy_language_model_analysis.md`](background/legacy_language_model_analysis.md) (frozen) |
| features document | [`background/modeling_solutions/essential_language_features.md`](background/modeling_solutions/essential_language_features.md) (frozen) |
| embeddings document | [`background/modeling_solutions/embeddings_and_vector_databases.md`](background/modeling_solutions/embeddings_and_vector_databases.md) (frozen) |
| legacy ideas | [`background/modeling_solutions/legacy_best_ideas.md`](background/modeling_solutions/legacy_best_ideas.md) (frozen) |

### 1.3 Identifiers

| ID | Meaning | Defined in |
|---|---|---|
| DEC-xx | a decision taken by Paolo | decision log §1 |
| PROP-xx | a proposal awaiting Paolo's confirmation | decision log §2 |
| Q-xx | an open question, with options and a recommendation | decision log §3 |
| RQ1–RQ6 | research questions | vision document §2 |
| P1–P12 | principles | vision document §4 |
| R1–R14 | requirements | validation document §1 |
| V1–V36 | validation targets: findings the model must reproduce | validation document §2 |
| H1–H3 | hypotheses to explore, not targets | validation document §2.4 |
| SM-01–SM-16 | submodels | conceptual model §7 |
| HOME, CARE, SCHOOL, UNIV, WORK, SERV, ADMIN, SOCIAL, PUBLIC, MEDIA | domain codes | domains document §0 |
| F1–F5 | the five essential language features | features document |
| A0, A1, A2, B0, C0 | first versions of the learning-core approaches A, B and C | LMNA §4–6 |
| S1–S17 | shortcomings of the legacy learner | LMNA §2.2 |
| M1–M13 | findings on the legacy memory rule | MMA |
| L1–L11 | weaknesses of the legacy language model | legacy analysis |
| X1–X8, D1–D11, N1–N32 | findings of the review | the review |
| D1–D3 | decision points of LMNA | LMNA §7.3 |
| G1–G5 | conditions of the embeddings gate | embeddings document |

**Clashes inherited from the frozen documents.** Always write the prefix that
tells them apart:

| Ambiguous | Write |
|---|---|
| A, B | **language A**, **language B** (the two languages) vs **approach A**, **approach B** (learning cores) |
| D1–D3 | **LMNA D1** (decision point) vs **review D1** (finding) |
| S1, S2 | **LMNA S1** (shortcoming) vs **semantics option S1** (Q-11; embeddings document) |

### 1.4 Literature

- In the text: author and year, e.g. De Houwer (2007). Three or more authors:
  the first author and "et al.".
- The full reference is in the **References** list at the end of the same
  document. A few documents point to another document's list instead (the
  validation document points to LMNA Appendix C for V1–V23).

### 1.5 Code

- `agent.py:1522` means file and line in the **legacy** repository at commit
  `b23edcd` (see [`background/README.md`](background/README.md)). This project
  has no code yet.

### 1.6 Symbols in equations

- Names like `β_stat`, `ρ` or `τ_fast` are the parameters and variables of one
  submodel. Each is defined in the parameter table of the document that
  introduces it (for the motives model: motives spec §3 and §7). Later they
  all go into the parameter register (validation document §5).
- `x_p(l)` means "x for person `p` and language `l`".

---

## 2. Terms

| Term | Meaning |
|---|---|
| **Accommodation** | Adjusting one's speech, including the choice of language, toward the interlocutor. Speakers of the lower-status language converge more (Communication Accommodation Theory; Giles et al., 1991). Catalonia's **accommodation norm** (Woolard, 1989) is one case. |
| **Attachment** | How much a person identifies with a language as "theirs". Formed mainly in childhood; one factor of the defence motive. |
| **Burn-in** | Running the generic world under a baseline scenario for one to two generations, so that founding conditions stop mattering, before scenarios start |
| **Compensation vs conformity** | Whether parents give the child the language the environment lacks (compensation) or the one it provides (conformity) |
| **Defence motive** | Choosing a language to protect it from assimilation: attachment × perceived threat |
| **Ethnolinguistic vitality** | A group's strength as a distinct language community: status, demography, institutional support (Giles, Bourhis & Taylor, 1977). Subjective vitality is how members perceive it. |
| **Generic world** | A synthetic society that is realistic in structure but not tied to a country, period or calendar years (DEC-08) |
| **Language-pair generator** | It produces synthetic language pairs from parameters (lexicon size, frequency structure, share of cognates, form distances), so results can be swept over linguistic distance (PROP-11) |
| **Perceived status** | The share of a language in a person's status-weighted experience: high if it dominates work, school, administration and media around them |
| **Perceived vitality, perceived threat** | How much a language is heard around a person now (fast average) and as remembered (slow average). Threat is the perceived decline between the two. |
| **Specific-society phase** | The later phase in which the model is correlated with one real society (Catalonia first), through its census, survey data and history |
| **Status and solidarity** | The two classic dimensions of language attitudes: prestige and usefulness vs identity and belonging (Ryan, Giles & Sebastian, 1982) |
| **Stylised fact** | A pattern reported across many societies (e.g. three-generation shift of immigrants), used as a qualitative target for the generic world |
| **Activity** | What people do in a setting, with an interaction structure (a lecture, a chat at break) |
| **Acceptance band** | The range a simulated result must fall in to pass a validation target. Fixed before fitting. |
| **Baseline learner** | A simple statistical learner (exposure → proficiency) that every richer learner must beat |
| **Cognate** | A translation pair with similar forms (`porta`/`puerta`). Strength is measured by form distance. |
| **Concept** | A meaning shared across languages, linked to one or more lemmas per language |
| **Contextual diversity** | The number of different contexts (e.g. films) a word occurs in. A better predictor of recognition than frequency. |
| **Coverage** | The share of running words (tokens) in speech that a listener knows. Comprehension needs about 95–98 %. |
| **Domain** | A sphere of life with its own participants and norms of language use: HOME, CARE, SCHOOL, UNIV, WORK, SERV, ADMIN, SOCIAL, PUBLIC, MEDIA |
| **Event** | One timestamped occurrence of an activity with its participants. The unit the learning core receives. |
| **Exposure** | The words a person hears and says, per language, register and day, directed or overheard |
| **False friend** | Similar forms with different meanings (Catalan `cama` "leg" vs Spanish `cama` "bed") |
| **Gate** | A check that must pass before the next phase or before a component enters the model |
| **History matching** | Ruling out parameter regions that cannot reproduce the targets, before fine fitting |
| **Initiator effect** | The person who opens an interaction influences its language |
| **Lemma** | A dictionary form of a word in one language (`anar`, `ir`) |
| **MAXIMIN** | Groups converge on the language best known by the least competent participant (Van Parijs, 2011) |
| **Perceived profile** | What an agent believes about another's languages: noisy, and updated by experience |
| **Permastore** | A long-term plateau of retention for well-learned material (Bahrick, 1984) |
| **Productive / receptive** | Able to say a word, vs able to understand it. Receptive knowledge is larger and more durable. |
| **Receptive multilingualism** | Each person speaks their own language and understands the other's (ten Thije & Zeevaert, 2007) |
| **Register** | The word distribution of a kind of speech: child-directed, academic, work by sector, conversational, media |
| **Relationship memory** | The language a pair or group has used, which tends to stick |
| **Retrievability** | The probability of recalling a word now, given its memory trace |
| **Setting** | A concrete instance of a domain: a place, a group, a time pattern (class 3B, Monday to Friday) |
| **Spin-up** | Building an initial agent's state by running the learner through a simulated personal history |
| **Transmission** | A parent's choice of language with their child. The decisive stage for a language's survival (Fishman, 1991). |
| **Virtual instrument** | A survey or test applied to simulated agents exactly as to people: virtual census, virtual EULP, virtual CDI |
| **EULP** | *Enquesta d'usos lingüístics de la població*: the survey of language use in Catalonia (Idescat and the Catalan government; 2003–2023) |
| **CDI** | MacArthur–Bates Communicative Development Inventories: parent checklists of words children understand and say |
| **LexTALE** | A short lexical-decision vocabulary test (Spanish version: LexTALE-Esp) |
| **ODD** | Overview, Design concepts, Details: the standard protocol for describing agent-based models (Grimm et al., 2020) |
| **SBI** | Simulation-based inference: estimating parameters when the likelihood is intractable but simulation is cheap |
| **IDs** | See §1.3 |
