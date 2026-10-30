**Research account:** this copy is published at [ec75hash/in-context-availability-moe-routing](https://github.com/ec75hash/in-context-availability-moe-routing). The [original repository](https://github.com/jeffreywilliamportfolio/in-context-availability-moe-routing) and its history remain available. [Archived paper v1.2](https://zenodo.org/records/23546831) · [Copy provenance](PUBLICATION_PROVENANCE.md).

# In-Context Availability Reorganizes Expert Routing: A Measurement Confound for Multi-Turn Evaluations of Mixture-of-Experts Language Models

Paper source, built PDF, and figure for **version 1.2 (October 2026)** of the paper, with the version 1.1 files kept for the record. Preprint, not peer reviewed.

**Version 1.2 withdraws the knockout and forcing results of versions 1.0 and 1.1.** The intervention code edited router logits that the model did not dispatch on, so no expert was excluded or forced; a code review found this on 2026-09-04 and it was reproduced on 2026-10-07. Version 1.2 replaces those results with a dispatch-verified follow-up on Qwen3.6-35B-A3B, records that layer 26 of this checkpoint is a trained copy of layer 14, and describes Expert 114 as one of several genre-selective experts at layer 14. All other reported values are unchanged.

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.21892999.svg)](https://doi.org/10.5281/zenodo.21892999)

**Author:** Jeffrey W. Shorthill (independent researcher) · ORCID [0009-0004-3954-2752](https://orcid.org/0009-0004-3954-2752)
**Concept DOI (resolves to the latest version):** [10.5281/zenodo.21892999](https://doi.org/10.5281/zenodo.21892999)
**Version 1.2 record DOI (2026-10-21):** [10.5281/zenodo.23546831](https://doi.org/10.5281/zenodo.23546831)  
**Version 1.1 record DOI (2026-08-24, superseded):** [10.5281/zenodo.22088887](https://doi.org/10.5281/zenodo.22088887)
**License:** [CC BY 4.0](LICENSE)

## What the paper claims

In a sparse mixture-of-experts (MoE) language model the router selects a small subset of
experts for every token, and that selection is increasingly read as an internal-state
measurement. The paper shows that one property of the preceding context, whether the text
being processed is already present verbatim in an earlier turn (in-context availability),
reorganizes routing at fixed token identity and fixed final prompt. In Qwen3.5-35B-A3B-Base,
teacher-forced response pairs differing only in the prior turn shifted layer-14 selection of
pre-specified register-specific expert sets by -0.175 (95% prompt-cluster bootstrap CI
[-0.184, -0.166]) and raised a pre-specified cross-register set by +0.058 ([0.055, 0.061]),
under expert sets, estimands, and decision rules fixed before capture. A 2x2 factorial
attributes the shift to literal availability of the target rather than prompt repetition,
and the shift survives matching on predictive entropy and target surprisal. Attention
retrieval of the prior copy carries about half of it: masking that attention moves layer-14
routing more than half of the way back to its no-availability configuration (12 of 12
pairs). The set structure replicates on instruction-tuned Qwen3.6-35B-A3B under seven
expert-level predictions fixed before capture (7 of 7 confirmed). Versions 1.0 and 1.1
reported that excluding or forcing the confirmed experts at layer 14 left generation
token-identical; that result is withdrawn in version 1.2, because the intervention code
edited router logits that the model did not dispatch on. In a corrected-implementation
follow-up (Qwen3.6-35B-A3B on an MLX build, dispatch verified, 12 prompts, greedy),
excluding the four increase-experts changed the generated text in seven of twelve prompts
without a detected average change in overlap with the available prior answer, and forcing
one increase-expert raised that overlap and changed eleven of twelve outputs. Layer 26 of
this checkpoint is a trained copy of layer 14, so the earlier layer-26 corroboration is the
same signature seen through a copy. The consequence is methodological: internal-state
measurements taken on multi-turn probes that place later target text in earlier context
partly measure availability in addition to the capability under test, and replicated
observational routing signatures do not by themselves license causal claims about the
experts involved.

## Repository layout

| Path | Contents |
|---|---|
| `paper/in-context-availability-moe-routing-v1.2.tex` | Paper source, version 1.2 (LaTeX, two-column; bibliography is inline). Identical to the file archived on Zenodo record 23546831. |
| `paper/in-context-availability-moe-routing-v1.2.pdf` | Built PDF, version 1.2, as archived on Zenodo record 23546831 (11 pages). |
| `paper/in-context-availability-moe-routing-v1.1.tex`, `.pdf` | Version 1.1 source and PDF, kept for the record; its intervention section is withdrawn (Zenodo record 22088887 carries a superseded-by note). |
| `paper/fig_clean_confirmation.pdf` | The paper's single figure (matched-token design and headline result). |
| `CITATION.cff` | Citation metadata. |
| `LICENSE` | CC BY 4.0. |

## Data

This repository holds no data. All raw router archives, token surfaces, compact results,
pre-specified analysis specifications, capture code, and the release-wide `SHA256SUMS`
manifest are in the HuggingFace dataset
[`ec75hash/qwen35-exact-turn-routing`](https://huggingface.co/datasets/ec75hash/qwen35-exact-turn-routing).
Version 1.2 of the paper cites tag `v1.3.1` of that dataset, which adds the dispatch-verified
intervention follow-up under `extension/20261007-dispatch-verified-interventions/` and a
withdrawal notice for the August knockout/boost captures:
<https://huggingface.co/datasets/ec75hash/qwen35-exact-turn-routing/tree/v1.3.1>
(Version 1.1 cited tag `v1.2`.)

## Related

Companion technical report (Expert 114 program compendium, re-opened 2026-10-21 with a status note):
[10.5281/zenodo.20709736](https://doi.org/10.5281/zenodo.20709736)

Repeated-block weight scan cited by version 1.2 for the layer-14/layer-26 relationship:
[10.5281/zenodo.23546828](https://doi.org/10.5281/zenodo.23546828) ·
[github.com/ec75hash/copy-blocks-qwen](https://github.com/ec75hash/copy-blocks-qwen)

Research releases from this author now live on [github.com/ec75hash](https://github.com/ec75hash).

## Rebuilding the PDF

The source is self-contained (no `.bib`, no external packages beyond a standard TeX Live).
The figure is loaded from the same directory via `\graphicspath{{figs/}{./}}`.

```bash
cd paper
latexmk -xelatex in-context-availability-moe-routing-v1.2.tex
```

The archived PDF was produced with XeLaTeX (`latexmk -xelatex`, TeX Live 2025); the
version 1.2 document is 11 pages.

## Citing

See [`CITATION.cff`](CITATION.cff). Cite the version 1.2 record DOI
[10.5281/zenodo.23546831](https://doi.org/10.5281/zenodo.23546831) for this version, or the
concept DOI [10.5281/zenodo.21892999](https://doi.org/10.5281/zenodo.21892999) for the
latest version.
