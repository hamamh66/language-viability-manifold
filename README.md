# Language on the Viability Manifold — companion repository

Companion code and results for the manuscript *Language on the Viability Manifold: A UVIF Framework for Emergent Linguistic Laws* (H. Hamam, Université de Moncton).

The repository contains the executable protocol (a single Google Colab notebook), the complete result tables and figures of the registered run reported in the paper, an independent GPU replication of Experiments A, B and the force-ratio sweep, and the LaTeX source of the manuscript.

## Layout

```
notebook/Language_Viability_Manifold.ipynb   the protocol (Colab; outputs to MyDrive/Outputs/Language_Viability_Manifold/)
results/config.json                          registered configuration of the reported run (SHA-256 printed at execution)
results/environment.json                     software environment of the reported run
results/outputs_summary.json                 single-source summary consumed by the Results section
results/expC_jacobian.json                   H7 intervention-response Jacobian
results/tables/*.csv                         every table cited in the paper (expA_, expB_, expC_, expD_, expH8_)
results/figures/*.pdf                        figures as they appear in the paper
results/replication_colab_gpu/               independent re-execution of A, B and the sweep on a Colab GPU
scripts/make_figures.py                      regenerates the paper figures from results/tables
paper/                                       LaTeX source (elsarticle), sections, bibliography, figures
```

## Reproducing the run

1. Open `notebook/Language_Viability_Manifold.ipynb` in Google Colab with a GPU runtime.
2. Cell 0 is preset to `QUICK = False`, `MODE = "full"`. `MODE` selects which stages run under *Run all*:
   `"full"` (registered grid), `"pilot_B"` (A and B only), and three diagnostic modes retained for the record
   (`"capacity_pilot"`, `"decoding_diagnostic"`, `"optimizer_pilot"`); diagnostic outputs are not confirmatory.
3. *Runtime → Run all*. The notebook mounts Drive and writes `config.json` (with its digest), `environment.json`,
   `tables/`, `figures/`, the fetched Universal Dependencies r2.18 test splits with SHA-256 digests, and
   `outputs_summary.json` under `MyDrive/Outputs/Language_Viability_Manifold/`. The full grid takes several hours;
   each stage writes its tables as it finishes, so a disconnected session can be resumed from the stalled cell.
4. `python scripts/make_figures.py` regenerates the figures from `results/tables` (edit the `R`/`OUT` paths at the top).

Set `QUICK = True` for a smoke test of the whole pipeline in a few minutes on CPU; its outputs are engineering diagnostics only.

## Evidence policy

Every number in the paper is traceable to a named CSV in `results/tables`. Thresholds, weights, scales, grids and seeds are fixed in the `CONFIG` cell before any experiment runs. The three full-length diagnostic pilots that preceded the registered configuration are described in the paper's Reproducibility section; they changed only condition-blind optimizer settings and never a threshold.

## Data

Corpora are the test splits of eight Universal Dependencies r2.18 treebanks (en_ewt, fr_gsd, de_gsd, es_gsd, ar_padt, zh_gsd, tr_imst, fi_tdt), fetched at run time from the UD GitHub repositories; URLs and file digests are recorded in `results/tables/expA_corpus_laws.csv`. They are not redistributed here; each treebank carries its own license.

## Citation

See `CITATION.cff`. Please cite the manuscript once a preprint or published version is available.

## License

Code and notebook: MIT (see `LICENSE`). Manuscript text and figures: © H. Hamam, all rights reserved pending publication.
