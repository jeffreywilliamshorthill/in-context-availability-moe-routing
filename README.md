# In-Context Availability Reorganizes Expert Routing: A Measurement Confound for Multi-Turn Evaluations of Mixture-of-Experts Language Models

Paper source, built PDF, and figure for version 1.1 (August 2026) of the paper. Preprint, not peer reviewed.

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.21892999.svg)](https://doi.org/10.5281/zenodo.21892999)

**Author:** Jeffrey W. Shorthill (independent researcher) · ORCID [0009-0004-3954-2752](https://orcid.org/0009-0004-3954-2752)
**Concept DOI (resolves to the latest version):** [10.5281/zenodo.21892999](https://doi.org/10.5281/zenodo.21892999)
**Version 1.1 record DOI (2026-08-24):** [10.5281/zenodo.22088887](https://doi.org/10.5281/zenodo.22088887)
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
expert-level predictions fixed before capture (7 of 7 confirmed), yet excluding or forcing
the confirmed experts at layer 14 during generation leaves output token-identical in every
prompt tested. The consequence is methodological: internal-state measurements taken on
multi-turn probes that place later target text in earlier context partly measure
availability in addition to the capability under test, and replicated observational routing
signatures do not by themselves license causal claims about the experts involved.

## Repository layout

| Path | Contents |
|---|---|
| `paper/in-context-availability-moe-routing-v1.1.tex` | Paper source (LaTeX, two-column; bibliography is inline). Identical to the file archived on Zenodo record 22088887. |
| `paper/in-context-availability-moe-routing-v1.1.pdf` | Built PDF as archived on Zenodo record 22088887. |
| `paper/fig_clean_confirmation.pdf` | The paper's single figure (matched-token design and headline result). |
| `CITATION.cff` | Citation metadata. |
| `LICENSE` | CC BY 4.0. |

## Data

This repository holds no data. All raw router archives, token surfaces, compact results,
pre-specified analysis specifications, capture code, and the release-wide `SHA256SUMS`
manifest are in the HuggingFace dataset
[`ec75hash/qwen35-exact-turn-routing`](https://huggingface.co/datasets/ec75hash/qwen35-exact-turn-routing).
The paper cites tag `v1.2` of that dataset:
<https://huggingface.co/datasets/ec75hash/qwen35-exact-turn-routing/tree/v1.2>

## Related

Companion technical report (Expert 114 program compendium):
[10.5281/zenodo.20709736](https://doi.org/10.5281/zenodo.20709736)

## Rebuilding the PDF

The source is self-contained (no `.bib`, no external packages beyond a standard TeX Live).
The figure is loaded from the same directory via `\graphicspath{{figs/}{./}}`.

```bash
cd paper
latexmk -pdf in-context-availability-moe-routing-v1.1.tex
```

The archived PDF was produced with XeLaTeX (`latexmk -xelatex`); both engines build the
same 9-page document from this source.

## Citing

See [`CITATION.cff`](CITATION.cff). Cite the version 1.1 record DOI
[10.5281/zenodo.22088887](https://doi.org/10.5281/zenodo.22088887) for this version, or the
concept DOI [10.5281/zenodo.21892999](https://doi.org/10.5281/zenodo.21892999) for the
latest version.
