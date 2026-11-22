# Background documents (frozen)

These documents were written in the legacy repository
(`github.com/pgervila/bilingual_society_ABM_legacy`, branch
`feature/explore_new_modeling`, commit `128e3e9`, Nov 2026). They are copied
here as **frozen inputs**:
- do not edit them;
- record any change of mind in [`../06_decisions.md`](../06_decisions.md);
- record changes of design in the living documents in `docs/`.

**References.** Code references such as `agent.py:1522` and links to
`docs/components/` point to the legacy repository at commit `b23edcd`. Two
links in `memory_model_analysis.md` were rewritten to GitHub URLs. No other
text was changed.

## What each document is

| Document | Content | IDs it defines |
|---|---|---|
| [`legacy_language_model_analysis.md`](legacy_language_model_analysis.md) | The legacy language model as a whole: word representation, memory, speaking and listening, code-switching, MAXIMIN, how bilingualism emerges, weaknesses | weaknesses 1–11 (cited as L1–L11) |
| [`memory_model_analysis.md`](memory_model_analysis.md) | In-depth analysis of the legacy per-word memory rule, with worked numbers | findings **M1–M13**; targets V1–V10 |
| [`learning_model_new_approaches.md`](learning_model_new_approaches.md) | The redesign proposal: shortcomings, requirements, shared foundations, approaches A / B / C | **S1–S17**, **R1–R8**, **V1–V18**, LMNA decision points D1–D3 |
| [`learning_model_docs_review.md`](learning_model_docs_review.md) | A review of the two documents above | **X1–X8**, **D1–D11**, **N1–N32** |
| [`modeling_solutions/README.md`](modeling_solutions/README.md) | Index and conclusions of the modelling-solutions documents | — |
| [`modeling_solutions/embeddings_and_vector_databases.md`](modeling_solutions/embeddings_and_vector_databases.md) | Are embeddings and vector databases needed? (No; embeddings optional and gated) | gate conditions G1–G5 |
| [`modeling_solutions/essential_language_features.md`](modeling_solutions/essential_language_features.md) | Five essential language features and how to model them without embeddings | **F1–F5**, **V19–V23** |
| [`modeling_solutions/legacy_best_ideas.md`](modeling_solutions/legacy_best_ideas.md) | The legacy ideas worth carrying forward, across the whole model | — |

The living documents cite these as **MMA** (memory model analysis), **LMNA**
(new approaches), **the review**, and by file name for the modelling-solutions
documents.

## Status of their recommendations

Some recommendations were superseded later. When a background document and a
living document disagree, the living document wins.

| Recommendation | Where | Status now |
|---|---|---|
| Keep the legacy learner as a `legacy` plug-in and compare against it | LMNA §3.1 rule 4, §3.3, §7.2 | **Dropped.** No legacy code in the new project ([`../06_decisions.md`](../06_decisions.md), DEC-04). |
| Apply "corrected legacy" fixes (Option A) to the legacy rule | MMA §4.2 | **Not applicable** (no legacy code). The analysis still explains *why* the new rule must differ. |
| FSRS-style rule (MMA) vs ACT-R (LMNA) | MMA §4.4; LMNA §4.3; review X1, N1–N4 | **Open.** Compare the candidates in a bake-off at the first learning-core gate (Q-08). |
| Embeddings for semantic fields and context in A1 | LMNA §4.7 | **Reduced.** Explicit per-setting counts by default; embeddings only behind a gate (`embeddings_and_vector_databases.md`). |
| A0 lexicon of 5,000 lemmas per language | LMNA §4.9; review N11 | **Open** (Q-09) |
| Catalan–Spanish as the reference case | LMNA §3.2, §8 | **Decided, generalised** (DEC-07). The first reference pair; language pairs are parameters. |
| Population validation on census and EULP (V17) as part of the first build | LMNA §3.5, §7.2 | **Deferred** (DEC-08) to the specific-society phase. The generic world is tested on stylised facts first. |
| Social layer "kept as is" | LMNA §2.1 | **Superseded.** The social layer is rebuilt from the legacy *ideas*, with new society domains ([`../02_society_domains.md`](../02_society_domains.md)). |
