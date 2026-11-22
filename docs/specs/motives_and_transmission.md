# Language motives and intergenerational transmission (SM-16, SM-03)

> **Status:** specification draft v0 (2026-11-21), for discussion. It answers
> DEC-09 in [`../06_decisions.md`](../06_decisions.md). Parents mostly pass on
> the language they are most proficient in, or the one they perceive as more
> prestigious, or the one they want to defend against assimilation. A single
> "loyalty" trait is not enough.
>
> This document specifies:
> - **SM-16, language perceptions and motives:** what each person perceives
>   about each language, and how;
> - **SM-03, transmission:** how parents choose the language for a child.
>
> The same perceptions also feed everyday language choice (SM-11, §6).
>
> Languages are labelled **A** and **B** throughout, as the model is
> language-agnostic (DEC-07). In the reference case, A and B are Catalan and
> Spanish.

---

## 0. Summary

A parent's choice of language for a child combines three **motives** and two
**constraints**:

| | Term | Meaning | What changes it |
|---|---|---|---|
| Motive | **Proficiency** | the language the parent speaks best and most comfortably | exposure and memory (learning core) |
| Motive | **Status** | the language the parent perceives as more prestigious or useful | the parent's experience of which language dominates high-status domains: work, school, administration, media |
| Motive | **Defence** | the language the parent wants to protect from assimilation | **attachment** to the language (formed mainly in childhood) × **perceived threat** (perceived decline of the language around them) |
| Constraint | **Couple** | the language the partners share | partnering; the couple's history |
| Constraint | **Environment** | what the child will get anyway outside the home (school, neighbourhood) | policy; local composition |

**Status, attachment and threat are not fixed traits.** They are perceptions
built from each person's own experience in the model. This keeps the model
general (DEC-08): no culture-specific constants are needed, only the weights
of the motives and the timescales of perception.

The choice is a **probabilistic discrete choice** (multinomial logit) among
A, B, or both, restricted to the languages the parent can speak.

The same perceptions, with their own weights, enter **everyday language
choice**. For example, a strongly attached speaker who perceives a threat may
refuse to accommodate.

Three feedback loops follow:
- **status:** reinforcing, it drives shift;
- **competence:** reinforcing, it drives shift;
- **defence:** balancing, it slows or reverses shift.

Their balance decides whether bilingualism is stable, shifts, or recovers.

---

## 1. Why not a single "loyalty" trait

The three motives have **different causes, different dynamics and different
responses to policy**. A single trait cannot tell them apart:

| Motive | Changes when… | A policy that acts on it |
|---|---|---|
| Proficiency | exposure changes: school, work, partner, media | medium of instruction; adult classes |
| Status | a language gains or loses ground in high-status domains | language requirements at work and in public services; media offer |
| Defence | people see their language decline around them, and care about it | visibility and support policies; also *unintended*: visible decline can trigger mobilisation |

A model with only "loyalty" would predict that raising a language's status
and teaching it more have the same effect. They may not. Separating the
motives is what lets the model say why a policy works, or does not.

---

## 2. Theoretical basis

| Element | Basis |
|---|---|
| Proficiency and comfort; the language of emotion with one's children | Pavlenko (2004); De Houwer (2007): children use a language actively most often when both parents speak it at home |
| Status (prestige, usefulness) | the **status** dimension of language attitudes (Ryan, Giles & Sebastian, 1982); instrumental motivation (Gardner, 1985); the status parameter of language-competition models (Abrams & Strogatz, 2003) |
| Defence (solidarity under threat) | the **solidarity** dimension of attitudes (Ryan et al., 1982); integrative motivation (Gardner, 1985); **ethnolinguistic vitality** (Giles, Bourhis & Taylor, 1977) and its subjective perception (Bourhis, Giles & Rosenthal, 1981); reversing language shift (Fishman, 1991) |
| Decision within the family | family language policy: beliefs, practices and management (Spolsky, 2004; King, Fogle & Logan-Terry, 2008) |
| Choice model | multinomial logit (McFadden, 1974) |

---

## 3. Perceptions (SM-16)

Each person `p` holds, for each language `l`, the quantities below. All of
them update from the **events** the person takes part in or overhears (the
domains document §4.3), so they need no external data.

| Variable | Meaning | Range | Update |
|---|---|---|---|
| `prof_p(l)` | productive proficiency | 0–1 | from the learning core (cached proficiency) |
| `status_p(l)` | perceived status: the share of `l` in the person's **status-weighted** experience | 0–1 | exponential moving average (EMA), timescale `τ_s` |
| `vit_fast_p(l)` | perceived vitality now: the share of `l` in the speech the person hears around them | 0–1 | EMA, timescale `τ_fast` (about 1–2 years) |
| `vit_slow_p(l)` | perceived vitality as remembered: "how it used to be" | 0–1 | EMA, timescale `τ_slow` (about 15–20 years) |
| `threat_p(l)` | perceived decline | 0–1 | `max(0, vit_slow − vit_fast) / vit_slow` |
| `attach_p(l)` | identity attachment to `l` | 0–1 | formed mainly in childhood (§3.3) |

### 3.1 Perceived status

Each event `e` has a status weight `w(domain_e)`.
- In v0 there are two levels: **public and institutional** (WORK, SCHOOL, UNIV,
  ADMIN, MEDIA) with weight `ρ > 1`, and **private** (HOME, SOCIAL, PUBLIC,
  SERV) with weight 1.
- `status_p(l)` is the EMA of `w(domain_e)·[language_e = l]`, divided by the
  EMA of `w(domain_e)`.
- So a person who meets `l` mostly at work, in class and in the media perceives
  it as high-status, even if it is rare at home.
- Official status needs no separate parameter. It enters through ADMIN, MEDIA
  and SCHOOL events.

### 3.2 Perceived vitality and threat

`vit_p(l)` is the share of `l` among all the speech the person hears, smoothed
on two timescales.

`threat_p(l)` is positive when the language is heard *less now than before*,
which is how people perceive decline. It has two natural consequences:
- **Older people perceive more decline** in a shifting society, because their
  slow average remembers a past with more use.
- **People who move** into an area where their language is weaker perceive a
  threat at once.

### 3.3 Attachment

- At birth, `attach(l)` is the mean of the parents' attachments.
- During a **formative window** (age < `a_form`, about 18):

  ```
  attach(l) ← (1 − η)·attach(l) + η·[γ·attach_parents(l) + (1 − γ)·affective_share(l)]
  ```

  where `affective_share(l)` is the share of `l` in HOME and SOCIAL input.
- Afterwards it drifts slowly (rate `η_adult`, set to 0 in v0).

Attachment is mainly socialised, but experience in childhood matters, through
friends and school life. Whether attachment also reacts to threat in
adulthood ("reactive identity") is an open question (§9).

---

## 4. The transmission decision (SM-03)

### 4.1 When

- At each **birth**, each parent decides the language they will speak to the
  child.
- The decision sets the starting language of the parent–child relationship,
  with high stickiness.
- Later change goes through renegotiation (SM-11). From about school age,
  renegotiation includes the **child's own** motives: children can push a
  relationship toward their preferred language.

### 4.2 Options

A parent `p` can choose:
- `l` only if `prof_p(l) ≥ θ_tr`: no one transmits a language they cannot
  speak well enough;
- **AB** (both languages) only if both pass the threshold.

### 4.3 Utilities

```
U_p(l)  = β_prof·prof_p(l)
        + β_stat·status_p(l)
        + β_def·attach_p(l)·threat_p(l)
        + β_cpl·[l is the couple's language]
        + β_env·env_p(l)

U_p(AB) = ½·[U_p(A) + U_p(B)] + β_bil

P(choose o) = exp(U_p(o)) / Σ_{o' allowed} exp(U_p(o'))
```

- `env_p(l)` is the child's expected exposure to `l` outside the home: the
  school's instruction share plus the local share.
  - `β_env > 0` means **conformity**: give the child the language of the
    environment.
  - `β_env < 0` means **compensation**: the environment will provide it, so
    the home provides the other language.
  - Both happen in real families. The sign is an empirical question to
    explore, and it is set to 0 in v0.
- `β_bil` is the value a parent places on raising a bilingual child. It can be
  of either sign.
- Partners decide independently, each with the couple term. The family
  pattern **emerges**: both A, both B, one language per parent, or one parent
  using both.
- The child has no language label. Its profile is whatever it learns from its
  input (learning core).

### 4.4 Other relatives

- **v0:** grandparents, uncles and aunts speak to the child in the language of
  the linking parent, if they speak it well enough (the legacy rule).
- **v1:** they use the same utility model with their own perceptions.

---

## 5. Feedback loops

| Loop | Mechanism | Sign |
|---|---|---|
| **Status** | `l` dominates high-status domains → perceived status of `l` rises → more transmission of `l` → more speakers → more use in all domains | reinforcing: drives shift |
| **Competence** | less transmission of `l` → lower proficiency in the next generation → fewer parents able to transmit `l` (threshold `θ_tr`) | reinforcing: drives shift |
| **Defence** | visible decline of `l` → threat rises → strongly attached speakers transmit and maintain `l` more → decline slows | balancing |

Stable bilingualism, shift and revitalisation are the outcomes of different
balances between these loops. That is a hypothesis the generic world can
explore (Phase 4).

---

## 6. The same motives in everyday language choice (SM-11)

Steps 3–5 of the order for resolving a conversation's language (domains
document §4.1) become a **motive-weighted choice**. The speaker chooses among
the languages the group can follow:

```
V_p(l) = α_acc·accommodation_p(l)               # toward the interlocutors' perceived language (MAXIMIN)
       + α_stat·status_p(l)·[public domain]
       + α_def·attach_p(l)·threat_p(l)          # maintenance: refusing to accommodate
       + α_mem·[l is the relationship's language]
```

- **Separate weights (`α`) from those of transmission (`β`).** A choice for a
  child's life and a choice in a shop are different decisions, made with the
  same perceptions.
- This produces non-accommodation (keeping one's own language with outsiders)
  without any culture-specific rule.
- It produces the accommodation asymmetry of Communication Accommodation
  Theory (Giles, Coupland & Coupland, 1991): speakers of the lower-status
  language converge more.

---

## 7. Parameters (v0)

| Symbol | Meaning | Prior or constraint | v0 |
|---|---|---|---|
| `β_prof` | weight of proficiency | > 0 | free |
| `β_stat` | weight of status | ≥ 0 | free |
| `β_def` | weight of defence | ≥ 0 | free |
| `β_cpl` | weight of the couple's language | ≥ 0 | free |
| `β_env` | conformity (+) or compensation (−) | any sign | 0 |
| `β_bil` | value of raising a bilingual child | any sign | free |
| `θ_tr` | minimum proficiency to transmit | 0–1 | from the learning core's "speaks" level |
| `ρ` | status weight of public over private domains | > 1 | free |
| `τ_s`, `τ_fast`, `τ_slow` | perception timescales | years; `τ_fast` < `τ_slow` | `τ_s = τ_fast` |
| `a_form`, `η`, `γ` | formation of attachment | `a_form` about 18; 0 < `η`, `γ` < 1 | free |
| `η_adult` | adult drift of attachment | ≥ 0 | 0 |
| `α_acc`, `α_stat`, `α_def`, `α_mem` | everyday choice | ≥ 0 | free |

**About 16 parameters**, 13 of them free in v0. In the generic world they are
explored over plausible ranges with a global sensitivity analysis. They are
calibrated later on data from a specific society.

---

## 8. Tests

**Behavioural unit tests** (deterministic expectations):
1. A parent below `θ_tr` in `l` never transmits `l`.
2. All else equal, a higher `status_p(A)` raises `P(A)` monotonically. The same
   holds for proficiency, and for attachment × threat.
3. A threat without attachment has no effect, and attachment without threat
   has no defence effect.
4. A symmetric parent (equal proficiency and perceptions) gives `P(A) = P(B)`.

**Generic stylised facts** (validation targets V31–V36 in
[`../04_requirements_and_validation.md`](../04_requirements_and_validation.md)):
- the proficiency pattern, and the "both parents" pattern (De Houwer, 2007);
- the status gradient;
- the three-generation shift of immigrants;
- domains retreating in order;
- the accommodation asymmetry;
- S-shaped shift.

**Hypothesis to explore, not a target:** perceived threat among strongly
attached speakers raises maintenance. The evidence is mixed, so it is tested in
the specific-society phase.

**Measurable counterparts**, so the motives can be tested against surveys
later:

| Model variable | Survey counterpart |
|---|---|
| `status_p(l)` | attitude items on usefulness and prestige |
| `attach_p(l)` | identification language; "my own language" items |
| `vit_p(l)`, `threat_p(l)` | subjective vitality questionnaires (Bourhis et al., 1981); "is the language's use increasing or decreasing?" items |
| transmission | the language spoken with one's children vs with one's parents |

The virtual survey instruments (SM-15) must produce these items from the
model's state.

---

## 9. Open questions

1. **Re-evaluation.** Should parents re-decide at milestones (school entry),
   or only through renegotiation? *Recommendation:* renegotiation only, with
   child agency from about 5–6 years.
2. **Separate weights** for transmission and everyday choice?
   *Recommendation:* yes (§6).
3. **Status weights:** two levels or per domain? *Recommendation:* two in v0.
4. **Reactive identity:** does attachment rise with threat in adults?
   *Recommendation:* not in v0; a v1 hypothesis.
5. **Resignation:** when vitality is very low, does defence give way to
   resignation? It would make the effect of threat non-monotonic.
   *Recommendation:* a v1 hypothesis.
6. **Compensation vs conformity** (the sign of `β_env`). *Recommendation:*
   explore both in the generic world.

## References

- Abrams, D. M., & Strogatz, S. H. (2003). Modelling the dynamics of language death. *Nature*, 424, 900.
- Bourhis, R. Y., Giles, H., & Rosenthal, D. (1981). Notes on the construction of a 'subjective vitality questionnaire' for ethnolinguistic groups. *Journal of Multilingual and Multicultural Development*, 2(2).
- De Houwer, A. (2007). Parental language input patterns and children's bilingual use. *Applied Psycholinguistics*, 28(3).
- Fishman, J. A. (1991). *Reversing Language Shift*. Multilingual Matters.
- Gardner, R. C. (1985). *Social Psychology and Second Language Learning*. Edward Arnold.
- Giles, H., Bourhis, R. Y., & Taylor, D. M. (1977). Towards a theory of language in ethnic group relations. In H. Giles (ed.), *Language, Ethnicity and Intergroup Relations*. Academic Press.
- Giles, H., Coupland, N., & Coupland, J. (1991). Accommodation theory: communication, context, and consequence. In *Contexts of Accommodation*. Cambridge University Press.
- King, K. A., Fogle, L., & Logan-Terry, A. (2008). Family language policy. *Language and Linguistics Compass*, 2(5).
- McFadden, D. (1974). Conditional logit analysis of qualitative choice behavior. In P. Zarembka (ed.), *Frontiers in Econometrics*. Academic Press.
- Pavlenko, A. (2004). 'Stop doing that, ia komu skazala!': language choice and emotions in parent–child communication. *Journal of Multilingual and Multicultural Development*, 25(2–3).
- Ryan, E. B., Giles, H., & Sebastian, R. J. (1982). An integrative perspective for the study of attitudes toward language variation. In E. B. Ryan & H. Giles (eds.), *Attitudes towards Language Variation*. Edward Arnold.
- Spolsky, B. (2004). *Language Policy*. Cambridge University Press.
