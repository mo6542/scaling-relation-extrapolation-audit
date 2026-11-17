# Scaling-relation extrapolation audit (pure metal → binary alloy)

Code, results and figures for the study *Error laws, mechanism and compute allocation when
extrapolating pure-metal scaling relations to binary alloys*.

**What this is.** A scaling relation fitted on pure metals is routinely reused to predict
adsorption energies on binary alloys. This package quantifies what that step costs, on
17,327 published DFT adsorption energies covering 303 transition-metal surfaces, and turns
the result into an operating rule for finite compute budgets.

**Headline numbers (all reproducible from the bundled results).**

| quantity | value |
|---|---|
| cross- vs same-bonding-centre extrapolation gap, surface level | **+0.471 eV** (95% CI [0.406, 0.532], 93/100 surfaces agree in sign) |
| same difficulty-matched (1:3 / 1:5) | +0.217 / +0.243 eV |
| adsorbate-cluster bootstrap (accounting for shared adsorbates) | [0.162, 0.808] eV |
| error spread across bonding-centre groups | 0.23 eV (S–S) … 1.46 eV (C–O), max 2.20 eV (CH–O) |
| compute budget: per-pair fitting (k=0) vs generic ML | 0.755 vs 0.891–0.902 eV MAE |
| compute budget: residual learning at k=100 alloy points | 0.603 eV MAE (≈80 h DFT) |

**Layout.** `run_all.py` is the single entry point. Analysis scripts are numbered in
dependency order; result files (`*.json`, `*.csv`) and figures (`fig_*.png`) are included so
that the numbers can be checked without re-running DFT or re-downloading the raw database.

**Quick check (no raw data needed).**

```bash
pip install -r requirements.txt
python run_all.py --check
```

**Full re-run** needs the raw records (`surf_pull.csv`, `surf_pull2.csv`, `surf_pull3.csv`)
fetched from [Catalysis-Hub](https://www.catalysis-hub.org) — they are **not** redistributed
here because of the source terms. Point `SCALING_DATA` at the directory holding them:

```bash
export SCALING_DATA=/path/to/cathub     # Windows: set SCALING_DATA=D:\path\to\cathub
python run_all.py
```

**Notes.**

- The audit scripts `42*`–`51*` validate every number in the manuscript against these result
  files. They read a snapshot of the manuscript text (`_corpus_legacy.md`); the manuscript
  itself is not part of this repository.
- Raw DFT structures, VASP inputs and the electronic-structure (PDOS) calculations are not
  included; the PDOS results are summarised in the manuscript and are exploratory only
  (the adsorbate SCF could not be converged).

**License.** Code: MIT. Derived data and figures: CC BY 4.0. Third-party raw data remains
under the original Catalysis-Hub terms.
